pipeline {
    agent any
    environment {
        SONARQUBE_TOKEN = credentials('sonarqube-token-id') // Configura las credenciales en Jenkins
        SONARQUBE_URL = 'http://4.204.40.19:9000'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('semestral2.0') { // Nombre de la configuración en Jenkins
                    sh """
                    sonar-scanner \
                    -Dsonar.projectKey=semestralciberV \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=${SONARQUBE_URL} \
                    -Dsonar.login=${SONARQUBE_TOKEN}
                    """
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
