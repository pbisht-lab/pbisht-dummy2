pipeline {
  parameters {
    string(name: 'DOCKER_IMAGE', defaultValue: 'docker-qa-local.docker.scm.tripwire.com/axon/jenkins2/axon-ruby-cookbooks:latest', description: 'Docker image to use.')
  }
  agent {
    docker {
      label 'docker'
      image params.DOCKER_IMAGE
    }
  }
  options {
    timeout(time: 1, unit: 'HOURS')
  }
  stages {
    stage('Publish to Chef Supermarket'){
      steps {
        // TODO handle uname(thru param?), don't use personel creds for authentication
        withCredentials([file(credentialsId: 'pbisht_public_supermarket', variable: 'KEY_FILE')]) {
          sh("chef exec stove --username pbisht --key $KEY_FILE --endpoint https://supermarket.chef.io/api/v1 --no-git --no-ssl-verify")
        }
      }
    }
  }
}
