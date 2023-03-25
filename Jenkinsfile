pipeline {
/*  agent {
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

*/ 
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
          - name: ubuntu
            image: ubuntu:latest
            command:
            - cat
            tty: true            
        '''
    }
  }
   stages {
    stage('clean workspace') {
      steps {
        cleanWs()
      }
    }
    stage('checkout') {
      steps {
        checkout scm
      }
    }
   
 stage('install make') {
     steps {
          container('ubuntu') {
            sh 'apt-get update && apt-get install make'
         }    
      }
    }     
    stage('verify make is installed') {
        steps {
          container('ubuntu') {
            sh 'make --version'
         }    
      }
    }
    stage('run make') {
        steps { 
           container('ubuntu') {
            sh 'make'
         }     
      }
    }
  } 
/*   
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
          sh ' echo Hello World > hello.txt'
          sh 'ls -last'
        }
        container('node') {
          sh 'npm version'
          sh 'cat hello.txt'
          sh 'ls -last'
        }
      }
    }
  }
*/ 
}
