Here is our pull requests pipeline:

![ss1](/ss1.png?raw=true)

[Link to pipeline yaml](/pipeline-pull-requests.yaml)

Successfully processed PRs look like this:

![ss2](/ss2.png?raw=true)

But there are numerous cases of this:

![ss3](/ss3.png?raw=true)

Note that the PR passed the linting and building jobs, but a deploy
job was never triggered.

The deploy job for this PR will never trigger, despite that there are no
relevant errors on the worker or web processes.

There are also numerous cases of this:

![ss4](/ss4.png?raw=true)

The PR will not undergo the linting or unit-testing jobs despite passing the
build job.

There are also numerous cases of this:

![ss5](/ss5.png?raw=true)

The PR will never even begin the build job at all.

At first we thought this may be an issue with the pull request Concourse resource:
https://github.com/jtarchie/github-pullrequest-resource/issues/178

But now I believe it is a more insidious issue with Concourse itself:
https://github.com/concourse/concourse/issues/1298

