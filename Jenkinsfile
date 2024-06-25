pipeline {
  agent any

  options {
    timeout(time: 9, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
    IMAGEN = "marianovmdocker/testapp"
    USUARIO = 'ID_US_DOCKER'
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
        script {
              echo "Deploying image: $IMAGEN:latest"
              docker.withRegistry( '', USUARIO ) {
                  docker.image("${IMAGEN}:latest").push()
                }
        }
      }
    }
}
}


    
  

