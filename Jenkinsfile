pipline { 

  aganet any 
  
  environment {
  
  DOCKERHUB_USER = 'YOUR_DOCKERHUB_USERNAME'
  IMAGE_NAME    = 'testingapp'
  K8S_NAMESPACE = 'default'
  
  }
  
  stages {
  
    stage ('checkout code') {
    
      steps {
      
      echo "clonning repository....."
      git branch: 'main', url: 'git@github.com:NourBkh/TestingApp.git'
      
      }
      
      
  
  }


}

post {

  always {
  
  echo "clinning up ..."
  sh 'docker system prune -f'
  
  }
  
  success { 
  
  echo "pipline is completed successfully yeeeyyy"
  
  }
  
  failure {
  
  echo "pipline failed oopss check logs"
  
  }



}


}




