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
    
    stage ('Cloning Git') {
      steps { 
        git 'https://github.com/Cesartrrs/ProyectoFinal'
      }
  }
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
