pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: ubuntu
            image: ubuntu:latest
            command:
            - cat
            tty: true
        '''
    }
  }
  stages {
/*    stage('clean workspace') {
      steps {
        cleanWs()
      }
    }
    stage('checkout') {
      steps {
        checkout scm
      }
    }
*/    
 stage('install make') {
      steps container('ubuntu') {
        sh 'apt update && apt install make'
      }
    }     
    stage('verify make is installed') {
      steps container('ubuntu') {
        sh 'make --version'
      }
    }
    stage('run make') {
      steps container('ubuntu') {
        sh 'make'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }   
}
