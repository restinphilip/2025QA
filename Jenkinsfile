pipeline{
  agent {
    label 'slave-1'
  }
  stage('custom_network'){
    steps{
      sh'''
      docker network create test --subnet=10.10.0.0/16 --gateway=10.10.0.1
      '''
    }
  }
  stage('docker_volume'){
    steps{
      sh'''
      docker volume create storage
      docker cp index.html storage
      '''
    }
  }
  stage('Httpd_container'){
    steps{
      sh'''
      docker run -dp 80:80  --name c1 --network test httpd -v storage:/usr/local/apache2/htdocs
      '''
    }
  }
}
