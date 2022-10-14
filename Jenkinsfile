node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonarqube';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
pipeline {
  agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3000:3000' 
        }
    }
  stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
    }
  agent any
 
  tools {nodejs "nodejs"}
 
  stages {
    stage('Unit Test') {
      steps {
        sh 'npm config ls'
      }
    }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
