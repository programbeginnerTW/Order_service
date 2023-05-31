pipeline{
  agent any
  stages{
    stage('verify tools'){
     steps{
     sh '''
      docker info
      docker version
      docker-compose version
     '''
     } 
    }
  }
}
