pipline { 

  aganet any 
  
  environment {
  
  DOCKERHUB_USER=
  IMAGE_NAME=
  K8S_NAMESPACE=
  
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




