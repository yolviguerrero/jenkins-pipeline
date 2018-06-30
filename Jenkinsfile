pipeline {
  agent any
  options {
      ansiColor('xterm')
      timestamps()
      timeout(time: 1, unit: 'HOURS')
  }

  stages {
    stage("Repository") {
      steps {
         // git url: "https://github.com/yolviguerrero/jenkins-pipeline.git"
	 checkout scm
      }
    }
    stage("Build") {
      steps {
        echo "build"
	sh "echo ${env.BUILD_NUMBER}"
	sh "echo ${env.JOB_NAME}"
	sh "echo ${env.BUILD_URL}"
	sh "echo ${env.WORKSPACE}"
      }
    }
    stage("Test") {
      steps {
        sh "echo tests"
      }
    }
    stage("Deploy") {
      steps {
        sh "echo deploy"
      }
    }
  } 
}

