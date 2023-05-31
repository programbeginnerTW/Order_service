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
        docker info
        docker version
        docker-compose version
       '''
     } 
    }
    stage('Clean all Docker containers'){
      steps{
        sh '''
          docker-compose down -v
          docker system prune -a --volumes -f
        '''
      }
    }
    stage('Start Container'){
      steps{
        sh '''
           docker-compose up -d
        '''
      }
    }
    stage('Dependency installation'){
      steps{
        sh '''
           docker exec -it order-service /bin/sh
           composer install
           exit
           docker-compose restart
        '''
      }
    }
    stage('Database migrate'){
      steps{
        sh '''
           sleep 2 
           docker exec -it order-service /bin/sh
           php spark migrate
           exit
           docker-compose up -d
        '''
      }
    }
    stage('Check life'){
        steps{
            sh '''
              curl localhost:8082/api/v1/order
            '''
        }
    }
  }
}
