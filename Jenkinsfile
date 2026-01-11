pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'nourbkh'
        IMAGE_NAME    = 'testingapp'
        K8S_NAMESPACE = 'default'
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning repository..."
                git branch: 'main', url: 'git@github.com:NourBkh/TestingApp.git'
            }
        }
        
        stage('install dependencies') {
          steps {
             dir('app') {
                echo "installing dependencies"
                sh 'npm install'
                }
          }
        }
        
        stage('build docker image') {
          steps {
             dir('app') {
              echo "building docker image"
              sh 'docker build -t $DOCKERHUB_USER/$IMAGE_NAME:latest .'
              }
          }
        }



    }

    post {
        always {
            echo "Cleaning up..."
            sh 'docker system prune -f'
        }
        success {
            echo "CI/CD pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs!"
        }
    }
}

