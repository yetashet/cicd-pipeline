pipeline {
    agent any
    environment {     
        DOCKERHUB_CREDENTIALS= credentials('hello')     
    }    
    stages {
        stage('Git Checkout') {
            steps {
                  git branch: 'main', url: 'https://github.com/Bakhytgul123/cicd-pipeline.git'

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

        stage('Node.js App Build') {
            steps {
                script {
                  sh 'docker build -t bakhazhi/jenkins_cicd_test_image .'
                  sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin docker.io'
                  sh 'docker push bakhazhi/jenkins_cicd_test_image'
                  sh 'docker logout' 
                }
            }
        }
    }
}
