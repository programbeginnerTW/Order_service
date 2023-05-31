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
           docker-compose exec -T order-service sh -c "composer install"
           docker-compose restart
        '''
      }
    }
    stage('Database migrate'){
      steps{
        sh '''
           sleep 2 
           docker-compose exec -T order-service sh -c "php spark migrate"
           docker-compose up -d
        '''
      }
    }
    stage('Check life'){
        steps{
            sh '''
              curl http://140.127.74.132:8082/api/v1/order
            '''
        }
    }
  }
}
