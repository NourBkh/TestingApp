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
        
        /*
        stage('pushing docker image') {
          steps {
             withCredentials([ usernamePassword( credentialsId: 'dockerhub', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASSWORD' ) ]) {
            echo "logging to dockerhub"
            sh 'echo \$DOCKERHUB_PASSWORD | docker login -u \$DOCKERHUB_USER --password-stdin'
            
            echo "pushing docker image to dockerhub"
            sh 'docker push $DOCKERHUB_USER/$IMAGE_NAME:latest'
            }
          }
        }
        */
        
        stage('Deploy to Minikube') {
          steps {
            echo "Deploying to Kubernetes..."
            sh """
                kubectl set image deployment/testingapp-deployment testingapp=$DOCKERHUB_USER/$IMAGE_NAME:latest -n $K8S_NAMESPACE
                
                kubectl rollout status deployment/testingapp-deployment -n $K8S_NAMESPACE

               """
               }
             }



    }

    post {
        always {
            echo "Cleaning up..."
        }
        success {
            echo "CI/CD pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs!"
        }
    }
}

