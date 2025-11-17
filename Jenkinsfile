pipeline {
  agent any

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
          docker-compose down -v || true
          docker volume rm storage || true
          docker volume create storage || true
          cp index.html /var/lib/docker/volumes/storage/_data
          chmod 644 /var/lib/docker/volumes/storage/_data/index.html
        '''
      }
    }

    stage('start-docker-compose') {
      steps {
        sh '''
          docker-compose -f docker-compose.yaml up -d one
        '''
      }
    }

  }
}
