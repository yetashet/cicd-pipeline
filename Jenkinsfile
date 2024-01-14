pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'chmod +x ./scripts/build.sh'
        sh 'bash ./scripts/build.sh'
      }
    }

    stage('test') {
      steps {
        sh 'chmod +x ./scripts/test.sh'
        sh 'bash ./scripts/test.sh'
      }
    }

    stage('docker') {
      environment {
        registry = 'deriterath/practice_task'
      }
      steps {
        script {
          checkout scm

          def customImage = docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

  }
  tools {
    nodejs 'nodejs'
  }
}
