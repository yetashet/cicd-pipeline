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

        stage('Node.js App Build') {
            steps {
                script {
                  sh 'docker build -t yediltashet/jenkins_image .'
                  sh 'echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --password-stdin docker.io'
                  sh 'docker push yediltashet/jenkins_image'
                  sh 'docker logout' 
                }
            }
        }
    }
}
