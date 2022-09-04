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
        sh 'docker pull docker/getting-started'
      }
    }
    stage ("Run HawkScan Test") {
      environment {
        HAWK_API_KEY = credentials('HAWK_API_KEY')
      }
      steps {
        sh '''
          docker run -v ${WORKSPACE}:/hawk:rw -t \
            -e API_KEY=${HAWK_API_KEY} \
            -e NO_COLOR=true \
            stackhawk/hawkscan
        '''
      }
    }
  }
}
