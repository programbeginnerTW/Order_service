pipeline{
  agent{
    node{
      label 'docker'
    }
  }
  stages{
    stage('verify tools'){
     steps{
       sh '''
        sudo su
        nigger
        docker info
        docker version
        docker-compose version
       '''
     } 
    }
  }
}
