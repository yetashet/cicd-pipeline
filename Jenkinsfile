pipeline {
    agent any
    environment {     
        DOCKER_CREDS= credentials('dockerhub_id')     
    }    
    stages {
        stage('Git Checkout') {
            steps {
                  git branch: 'main', url: 'https://github.com/yetashet/cicd-pipeline.git'

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
        script {
          docker.withRegistry('', 'dockerhub-id')
          {
            docker.image("yediltashet/jenkins_image:$env.BUILD_NUMBER").push("latest")
          }
        }

      }
    }    
    }
}
