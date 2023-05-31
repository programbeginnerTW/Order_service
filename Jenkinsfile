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
        sudo su -S nigger
        docker info
        docker version
        docker-compose version
       '''
     } 
    }
  }
}
