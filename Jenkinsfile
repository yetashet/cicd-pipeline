pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(branch: 'main', url: 'https://github.com/yetashet/cicd-pipeline.git')
      }
    }

    stage('App Build') {
      steps {
        sh 'script scripts/build.sh'
      }
    }

    stage('Tests') {
      steps {
        sh 'script scripts/test.sh'
      }
    }

    stage('Docker image build') {
      steps {
        sh 'docker build -t yediltashet/jenkins_image:$BUILD_NUMBER .'
      }
    }

    stage('Docker image deploy') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.io'
        sh 'docker push yediltashet/jenkins_image:$BUILD_NUMBER'
      }
    }

  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_id')
  }
}
