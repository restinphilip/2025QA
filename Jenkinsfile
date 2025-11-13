pipeline{
  agent {
    label 'qa'
  }
  stage('custom_network'){
    steps{
      sh'''
      docker network create test --subnet=10.10.0.0/16 --gateway=10.10.0.1 || true
      '''
    }
  }
  stage('copy_index') {
  steps {
    sh '''
    sudo mkdir -p /mnt/website || true
    rm -rf  /mnt/website/*
    sudo chmod -R 755 /mnt/website
    cp index.html /mnt/website
    '''
  }
}

  stage('Httpd_container'){
    steps{
      sh'''
       docker rm -f c1
       docker run -dp 80:80 --name c1 --network test -v /mnt/website:/usr/local/apache2/htdocs httpd
      '''
    }
  }
}
