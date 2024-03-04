pipeline {
      agent { label 'Dev' }
    
    stages {
        stage('Code') {
            steps {
                git url: 'https://github.com/ApurvDevops/node-todo-cicd.git', branch: 'master'
                echo 'Code clone  gya'
            }
        }
        stage('Build') {
            steps {
                sh "docker build -t node-app-test-new ."
                echo 'build ho gya'
            }
        }
        stage('Push Image') {
            steps { 
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser")]){
                sh "docker login -u${env.dockerhubuser} -p${env.dockerhubpass}"
                sh "docker tag node-app-test-new ${env.dockerhubuser}/node-app-test-new:latest"
                sh "docker push ${env.dockerhubuser}/node-app-test-new:latest"
                echo 'Push ho gya'
                }
            }
        }
        stage('deploy') {
            steps {
                sh  "docker-compose down && docker-compose up -d"
                echo 'deploy ho gya'
            }
        }
    }
}
