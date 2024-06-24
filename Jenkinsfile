pipeline {
  agent any

  options {
    timeout(time: 9, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  }
   stages {
   stage('Building image') {
      steps{
          echo "ETAPA Building Image"
          sh '''
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker tag testapp 127.0.0.1:5000/nuevavirtual/testapp
        docker push 127.0.0.1:5000/nuevavirtual/testapp   
        '''
        }
      }
    }
}


    
  

