# Jenkins Pipelines
## 1. Old ways
## 2. New ways
## 3. Requirements

1. Jenkins 2.x
2. DSL Plugins
## 4. Jenkins Job DSL Plug-In (Groovy Scripts)
1. Whats?

  1. The high-level DSL concepts are documented in [Job DSL
     Commands](https://github.com/jenkinsci/job-dsl-plugin/wiki/Job-DSL-Commands).
  2. See the [API Viewer](https://jenkinsci.github.io/job-dsl-plugin/) for a full syntax reference
  3. There are also tips on more advanced usage and workflows.

2. Example
  ```java
job('example') {
    logRotator(-1, 10)
    jdk('Java 6')
    scm {
        github('jenkinsci/job-dsl-plugin', 'master')
    }
    triggers {
        githubPush()
    }
    steps {
        gradle('clean build')
    }
    publishers {
        archiveArtifacts('job-dsl-plugin/build/libs/job-dsl.hpi')
    }
}
  ```

## Pipelines as a Code

	Definition of your build / pipeline will be stored together with your code as a Jenkinsfile


## Jenkins Jobs DSL Step

1. Stage

  Starts a new pipeline stage

  ```java
  stage 'Compile'
  node('java-build') {
    checkout scm
    sh 'mvn -B clean deploy'
    junit testResults: 'build/test-results/*xml'
  }

  stage 'Automated Tests'
  node ('qa-environments') {
      ...
  }
  ```

2. Node

  Execute steps on an agent (node) with the corresponding name / label
  ```java
  node('java-build') {
    checkout scm
    sh 'mvn -B clean deploy'
  }
  ```

3. Checkout

  Checkout code from SCM (GIT, SVN)
  ```
  node('java-build') {
    checkout scm
  }
  ```

  ```java
  node('java-build'){
    git url: 'git://github.com/engineerball/myproject.git',
        branch: 'develop',
        credentialsId: '12345-1234-4523-af123-1234572'
  }
  ```

4. Execute

  Execute command line or script

  ```java
  node('java-build') {
    stage 'Clean up workspace'
    sh 'rm -rf .'

    stage 'Checkout code'
    checkout
  }
  ```

5. Publishes

  Publish artifactory files

  ```java
  stage 'Compile'
  node('java-build') {
    checkout scm
    sh 'mvn -B clean deploy'
    junit testResults: 'build/test-results/*xml'
  }
  ```

## Pipelines examples
1. Working with files

  ```java
  //Write string to file
  WriteFile file: 'status.log', text: 'Status: OK', encoding: 'UTF-8'

  //Read file to string
  results = readFile file: 'results.log', encoding: 'UTF-8'

  //Example read XML file to string
  pom = readFile('pom.xml')
  matcher = (pom =~ '<version>(.+)</version>')
  version = matcher? matcher[0][1] : null
  ```

2. Pass files between stage

  ```java
  //Archive an artifact file to be use later
  stash name: 'artifact', includes: 'package-a.zip'

  //Get the artifact file e.g. on another node
  unstash 'artifact'

  //Stash multiple files:
  stash name: 'testResults',
        includes: '**/test-results/**.xml'
  ```

3. Parallel Execution of Steps

  ```java
  parallel(
    deployToEnv1: {
      node('environment-1') {
        deploy (...)
      }
    },
    deployToEnv2: {
      node('environment-2') {
        deploy (...)
      }
    }
  )
  ```

4. Use existing plugins in pipeline

  ```java
    slackSend channel: '#jenkins-latest',
              color: 'good',
              message: 'Slack Message',
              teamDomain: 'beedemo',
              token: 'token'
  ```
5. Manual steps - confirmation dialog

  ```java
    input message: 'Release to production?', ok: 'Release'
  ```

6. Docker Support

  ```java
    docker.image('java8-maven').inside {
      checkout scm
      sh 'mvn -B clean install'
    }
  ```

## How we use in DMP
