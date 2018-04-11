pipeline {
  environment {
    SOURCES_PREFIX = '/var/lib/jenkins/workspace/petclinic'
  }
  agent {
    docker {
      image 'java:8'
      args '-u 0:0'
    }
  }
  stages {
    stage('SCM checkout') {
      steps {
        checkout scm
        sh 'mkdir -p /root/src'
        sh 'cp -r . /root/src/'
      }
    }
    stage('Test') {
      steps {
        sh 'cd /root/src && pwd && ./mvnw test'
      }
    }
  }
  post {
    always {
      dir('/root/src') {
          junit "target/surefire-reports/*.xml"
      }
    }
  }
}
