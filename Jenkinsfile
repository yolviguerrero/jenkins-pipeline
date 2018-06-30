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
    booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Deploy to server')
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
      when {
        expression {
          return params.DEPLOY ==~ /(?i)(Y|YES|T|TRUE|ON|RUN)/
        }
      }
      steps {
        sh "echo deploy_servers"
      }
    }
  } 
}

