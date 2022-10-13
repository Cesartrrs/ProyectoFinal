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
  stage ('Unit Test') {
    def npmHome = tool 'nodejs';
    withnpm() { 
        sh "${npmHome}/usr/bin/node" 
    }''
  }
}
