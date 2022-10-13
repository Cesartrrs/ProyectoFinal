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
  agent any
 
  tools {nodejs "nodejs"}
 
  stages {
    stage('Unit Test') {
      steps {
        sh 'npm config ls'
        sh 'npm install'
        sh 'npm start'
      }
    }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
