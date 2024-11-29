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
  
  stage('Trigger Job B (cambio pagina web)') {
    steps {
        script {
            // Verifica el estado del análisis
            if (currentBuild.result == 'SUCCESS') {
                build job: 'Semestral-CiberV', wait: false
            } else {
                error('SonarQube analysis failed. Job B will not be triggered.')
            }
        }
    }
}
}
