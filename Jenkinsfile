pipeline {
  agent { label 'qa' }

  stages {

    stage('custom_network') {
      steps {
        sh '''
        sudo docker network create test --subnet=10.10.0.0/16 --gateway=10.10.0.1 || true
        '''
      }
    }
    stage('mk_docker_volume') {
      steps {
        sh '''
        docker volume create storage || true
        docker run -d--name temp -v storage:/usr/local/apache2/htdocs httpd
        docker cp index.html temp:/usr/local/apache2/htdocs/index.html 
        docker rm -f temp    
        '''
      }
    }

    stage('start-docker-compose') {
      steps {
        sh '''
        docker-compose -f docker-compose.yaml up start one-d
        '''
      }
    }

  }
}
