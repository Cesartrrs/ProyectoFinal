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
 
  stages ('unit test') {
  
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
