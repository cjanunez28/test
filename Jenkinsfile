node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonar-scanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"      
    }
  }
  
  stage('Trigger Semestral-CIberV') {
    steps {
        script {
            // Verifica el estado del análisis
            if (currentBuild.result == 'SUCCESS') {
                build job: 'Semestral-CiberV', wait: false
            } else {
                error('SonarQube analysis failed. Semestral-CIberV will not be triggered.')
            }
        }
    }
}
}
