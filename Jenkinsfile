node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv() {
      // sh "${scannerHome}/bin/sonar-scanner"
      bat "${scannerHome}/bin/sonar-scanner"
    }
  }
  
stage('Quality Gate') {
    timeout(time: 5, unit: 'MINUTES') {
        def qg = waitForQualityGate()
        if (qg.status != 'OK') {
            error "Quality Gate failed: ${qg.status}"
        }
    }
}

}
