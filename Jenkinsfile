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
    stages 
    {agent { node { label 'mocha-bdd' } } }{
		stage('Install dependencies') {
			steps {
				sh 'npm install --verbose'
			}
		}
		stage('Run lint') {
			steps {
				sh 'npm run lint'
			}
		}
		stage('Run tests') {
			steps {
				sh 'npm run test'
				sh '''
				cp ~/.coveralls.yml-mocha-bdd .coveralls.yml
				npm run cover
				'''
			}
		}
	}
	post {
		success {
			githubNotify context: 'continuous-integration/jenkins/mocha-bdd', description: 'The build passed.', status: 'SUCCESS'
		}
		failure {
			githubNotify context: 'continuous-integration/jenkins/mocha-bdd', description: 'The build failed.', status: 'FAILURE'
		}
		aborted {
			githubNotify context: 'continuous-integration/jenkins/mocha-bdd', description: 'The build was aborted.', status: 'ERROR'
		}
	}
}
}
