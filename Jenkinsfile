pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: node
            image: node:16-alpine3.12
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
