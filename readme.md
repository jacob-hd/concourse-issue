# What's the problem?
Concourse seems to be ignoring resources that are ready to be processed instead
of running the jobs that should be processing said resources.

This seems to happen often, without rhyme or reason, with the "Pull Request"
resource specifically.

Neither the `concourse-web` nor the `concourse-worker` services are reporting
any errors that seem to be related to this issue. The logs seem to indicate
all is well.

# Pipeline Structure
Here is our pull requests pipeline:

![ss1](/ss1.png?raw=true)

[Link to pipeline yaml](/pipeline-pull-requests.yaml)

# Successfully Processed PRs

Successfully processed PRs look like this:

![ss2](/ss2.png?raw=true)

# Unprocessed PRs - Case 1

![ss3](/ss3.png?raw=true)

Note that the PR passed the linting and building jobs, but a deploy
job was never triggered.

The deploy job for this PR will never trigger, despite that there are no
relevant errors on the worker or web processes.

# Unprocessed PRs - Case 2

![ss4](/ss4.png?raw=true)

The PR will not undergo the linting or unit-testing jobs despite passing the
build job.

# Unprocessed PRs - Case 3

![ss5](/ss5.png?raw=true)

The PR will never even begin the build job at all.

At first we thought this may be an issue with the pull request Concourse resource:

https://github.com/jtarchie/github-pullrequest-resource/issues/178

But now I believe it is a more insidious issue with Concourse itself:

https://github.com/concourse/concourse/issues/1298

