pipeline {
    agent any

    environment {
        DOCKERHUB_USER = 'YOUR_DOCKERHUB_USERNAME'
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

