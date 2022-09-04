pipeline {
  agent any
  stages {
    stage ("Checkout code") {
      steps {
        checkout scm
      }
    }
    stage ("Pull HawkScan Image") {
      steps {
        echo "hello world!"
        bat 'docker pull stackhawk/hawkscan'
      }
    }
    stage ("Run HawkScan Test") {
      environment {
        HAWK_API_KEY = credentials('HAWK_API_KEY')
      }
      steps {
        echo "hello world! 2"
        mkdir "~\.hawk"
        echo '$env:HAWK_API_KEY="hawk.ObHIhAiHte02lmPQTFov.lHymdViwtDBqkPcMISQN"' > $home\.hawk\hawk.ps1
        bat '''
          docker run -e API_KEY=$env:HAWK_API_KEY --rm -v ${PWD}:/hawk:rw -t stackhawk/hawkscan:latest
        '''
      }
    }
  }
}
