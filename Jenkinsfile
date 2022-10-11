node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonarqube';
    withSonarQubeEnv(
    sonar.projectKey=sonarproject2
    sonar.login=admin
    sonar.password=sonarpass
    sonar.sources=/var/lib/jenkins/workspace/
    sonar.host.url=http://35.247.2.163:9000) {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
