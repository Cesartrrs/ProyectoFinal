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
    stage('preflight') {
      steps {
        echo sh(returnStdout: true, script: 'env')
        sh 'node -v'
      }
    }
    stage('build') {
      steps {
        sh 'npm --version'
        sh 'git log --reverse -1'
        sh 'npm install'
      }
    }
    stage('test') {
      steps {
        sh 'npm config ls'
        sh 'npm install --global mocha'
        sh 'npm install --save-dev mocha'
        sh 'npm install mocha'
        sh 'cd /var/lib/jenkins/workspace/projectaccenture2/cidr_convert_api/node
        sh 'npm test'
      }
    }
  }
}
