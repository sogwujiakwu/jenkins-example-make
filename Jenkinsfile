pipeline {
  agent {
    docker {
        image 'ubuntu:latest'
        // Run the container on the node specified at the
        // top-level of the Pipeline, in the same workspace,
        // rather than on a new node entirely:
        reuseNode true
        args '--entrypoint='
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
        sh 'apt update && apt install make'
      }
    }    
    stage('verify make is installed') {
      steps {
        sh 'make --version'
      }
    }
    stage('run make') {
      steps {
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
