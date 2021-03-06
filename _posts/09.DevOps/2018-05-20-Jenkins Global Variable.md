---
title: "Jenkins Global Variable"
categories: DevOps
tags: [DevOps, Jenkins]
published: true
comments: true
---



> 해당글은 [Gloval Variables Reference](https://qa.nuxeo.org/jenkins/pipeline-syntax/globals) 글을 요약 정리한 글입니다.



## env

환경변수는 아래와 같이 사용할 수 있습니다.

```
mail to: 'devops@acme.com',
    subject: "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input",
    body: "Please go to ${BUILD_URL} and verify the build"
```



- BRANCH_NAME

  For a multibranch project, this will be set to the name of the branch being built, for example in case you wish to deploy to production from `master` but not from feature branches.

- CHANGE_ID

  For a multibranch project corresponding to some kind of change request, this will be set to the change ID, such as a pull request number.

- CHANGE_URL

  For a multibranch project corresponding to some kind of change request, this will be set to the change URL.

- CHANGE_TITLE

  For a multibranch project corresponding to some kind of change request, this will be set to the title of the change.

- CHANGE_AUTHOR

  For a multibranch project corresponding to some kind of change request, this will be set to the username of the author of the proposed change.

- CHANGE_AUTHOR_DISPLAY_NAME

  For a multibranch project corresponding to some kind of change request, this will be set to the human name of the author.

- CHANGE_AUTHOR_EMAIL

  For a multibranch project corresponding to some kind of change request, this will be set to the email address of the author.

- CHANGE_TARGET

  For a multibranch project corresponding to some kind of change request, this will be set to the target or base branch to which the change could be merged.

- BUILD_NUMBER

  The current build number, such as "153"

- BUILD_ID

  The current build ID, identical to BUILD_NUMBER for builds created in 1.597+, but a YYYY-MM-DD_hh-mm-ss timestamp for older builds

- BUILD_DISPLAY_NAME

  The display name of the current build, which is something like "#153" by default.

- JOB_NAME

  Name of the project of this build, such as "foo" or "foo/bar". (To strip off folder paths from a Bourne shell script, try: `${JOB_NAME##*/}`)

- BUILD_TAG

  String of "jenkins-*${JOB_NAME}*-*${BUILD_NUMBER}*". Convenient to put into a resource file, a jar file, etc for easier identification.

- EXECUTOR_NUMBER

  The unique number that identifies the current executor (among executors of the same machine) that’s carrying out this build. This is the number you see in the "build executor status", except that the number starts from 0, not 1.

- NODE_NAME

  Name of the slave if the build is on a slave, or "master" if run on master

- NODE_LABELS

  Whitespace-separated list of labels that the node is assigned.

- WORKSPACE

  The absolute path of the directory assigned to the build as a workspace.

- JENKINS_HOME

  The absolute path of the directory assigned on the master node for Jenkins to store data.

- JENKINS_URL

  Full URL of Jenkins, like `http://server:port/jenkins/` (note: only available if *Jenkins URL* set in system configuration)

- BUILD_URL

  Full URL of this build, like `http://server:port/jenkins/job/foo/15/` (*Jenkins URL* must be set)

- JOB_URL

  Full URL of this job, like `http://server:port/jenkins/job/foo/` (*Jenkins URL* must be set)



## currentBuild

currentBuild 변수는 현재 실행중인 빌드를 참조하는 데 사용될 수 있습니다. 다음과 같은 속성을 가지고 있습니다:

- number

  build number (integer)

- result

  typically `SUCCESS`, `UNSTABLE`, or `FAILURE` (*may* be null for an ongoing build)

- currentResult

  typically `SUCCESS`, `UNSTABLE`, or `FAILURE`. Will never be null.

- resultIsBetterOrEqualTo(String)

  Compares the current build result to the provided result string (`SUCCESS`, `UNSTABLE`, or `FAILURE`) and returns true if the current build result is better than or equal to the provided result.

- resultIsWorseOrEqualTo(String)

  Compares the current build result to the provided result string (`SUCCESS`, `UNSTABLE`, or `FAILURE`) and returns true if the current build result is worse than or equal to the provided result.

- displayName

  normally `#123` but sometimes set to, e.g., an SCM commit identifier

- description

  additional information about the build

- id

  normally `number` as a string

- timeInMillis

  time since the epoch when the build was scheduled

- startTimeInMillis

  time since the epoch when the build started running

- duration

  duration of the build in milliseconds

- durationString

  a human-readable representation of the build duration

- previousBuild

  another similar object, or null

- nextBuild

  similarly

- absoluteUrl

  URL of build index page

- buildVariables

  for a non-Pipeline downstream build, offers access to a map of defined build variables; for a Pipeline downstream build, any variables set globally on `env`

- changeSets

  a list of [changesets](http://javadoc.jenkins-ci.org/hudson/scm/ChangeLogSet.html) coming from distinct SCM checkouts; each has a `kind` and is a list of commits; each commit has a `commitId`, `timestamp`, `msg`, `author`, and `affectedFiles` each of which has an `editType` and `path`; the value will not generally be `Serializable` so you may only access it inside a method marked `@NonCPS`

- rawBuild

  a `hudson.model.Run` with [further APIs](http://javadoc.jenkins-ci.org/hudson/model/Run.html), only for trusted libraries or administrator-approved scripts outside the sandbox; the value will not be `Serializable` so you may only access it inside a method marked `@NonCPS`	