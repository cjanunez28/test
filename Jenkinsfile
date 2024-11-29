node {
    stage('SCM') {
        checkout scm
    }

    stage('SonarQube Analysis') {
        // Nombre del escáner configurado en Jenkins (asegúrate de usar el mismo)
        def scannerHome = tool name: 'semestral2.0', type: 'hudson.plugins.sonar.SonarRunnerInstallation'

        // Usa las credenciales y URL del servidor SonarQube configuradas en Jenkins
        withSonarQubeEnv('SonarQube') {
            // Ejecuta el análisis
            sh "${scannerHome}/bin/sonar-scanner"
        }
    }
}

