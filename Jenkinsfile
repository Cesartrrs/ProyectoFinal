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
        git 'https://github.com/Cesartrrs/ProyectoFinal/cidr_convert_api/node'
      }
  }
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh 'node test'
      }
    }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
