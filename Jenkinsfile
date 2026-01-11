pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'nourbkh'
        DOCKERHUB_PASSWORD = dockerhub''
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
        
        stage('pushing docker image') {
          steps {
            echo "logging to dockerhub"
            sh 'echo \$DOCKERHUB_PASSWORD | docker login -u \$DOCKERHUB_USER --password-stdin'
            
            echo "pushing docker image to dockerhub"
            sh 'docker push $DOCKERHUB_USER/$IMAGE_NAME:latest'
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

