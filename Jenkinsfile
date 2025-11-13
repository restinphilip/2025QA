pipeline{
  agent {
    label 'slave-1'
  }
  stage('custom_network'){
    steps{
      sh'''
      docker network create test --subnet=10.10.0.0/16 --gateway=10.10.0.1
      sh'''
    }
  }
  stage('docker_volume'){
    steps{
      sh'''
      docker create storage
      docker cp index.html storage
      sh'''
    }
  }
  stage('Httpd_container'){
    steps{
      sh'''
      docker run -dp 80:80  --name c1 --network test httpd -v velocity:/usr/local/apache2/htdocs
      sh'''
    }
  }
}
