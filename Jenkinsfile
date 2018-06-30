pipeline {
  agent any
  options {
    ansiColor('xterm')
    timestamps()
    timeout(time: 1, unit: 'HOURS')
  }
  environment {
    ARTIFACTOR = "${env.BUILD_NUMBER}.zip"
    SLACK_MESSAGE = "Job '${env.JOB_NAME}' Build ${env.BUILD_NUMBER}"
  }

parameters {
    string(name: 'SLACK_CHANNEL', defaultValue: '#deploys', description: '')
    choice(name: 'TYPE', choices: 'aut\ncron\ndata', description: 'Autoscaling, Cron or Data')
    booleanParam(name: 'LAUNCH_CONFIGURATION', defaultValue: false, description: 'Update aws new ami')
  }


  stages {
    stage("Repository") {
      steps {
          //git url: "https://github.com/mario21ic/jenkins-pipeline.git"
          checkout scm
      }
    }
    stage("Build") {
      steps {
        echo "build"
        sh "echo ${env.BUILD_NUMBER}"
        sh "echo ${env.ARTIFACTOR}"
        sh "touch ${ARTIFACTOR}"

    script {
          def ID = sh(returnStdout: true, script: "./ami_id.sh").trim()
          sh "./build_ami.sh ${ID}"
        }


      }
    }
    stage("Test") {
      steps {
 parallel (
          syntax: { sh "echo syntax" },
          grep: { sh "echo 'grep'" }
        )
      }
    }
    stage("Deploy") {
      steps {
        sh "echo deploy"
        archiveArtifacts artifacts: "${ARTIFACTOR}", onlyIfSuccessful: true
      }
    }
  } 
}

