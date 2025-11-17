pipeline {
  agent any

  stages {

    stage('mk_docker_volume') {
      steps {
        sh '''
          docker-compose down -v || true
          docker volume rm storage2
          docker volume create storage2 || true
          cp index.html /var/lib/docker/volumes/storage/_data
          chmod 644 /var/lib/docker/volumes/storage/_data/index.html
        '''
      }
    }

    stage('start-docker-compose') {
      steps {
        sh '''
          docker-compose -f docker-compose.yaml up -d three
        '''
      }
    }

  }
}
