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

