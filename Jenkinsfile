pipeline {
  agent any
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
	sh "echo ${JOB_NAME}"
	sh "echo ${BUILD_URL}"
	sh "echo ${WORKSPACE}"
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

