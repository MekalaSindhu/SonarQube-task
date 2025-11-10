pipeline {
    agent any

    environment {
        SCANNER_HOME = tool 'SonarScanner'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/MekalaSindhu/SonarQube-demo.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    bat "${SCANNER_HOME}\\bin\\sonar-scanner -Dsonar.projectKey=SonarQube-demo -Dsonar.sources=. -Dsonar.host.url=http://192.168.0.100:9000 -Dsonar.login=%SONAR_AUTH_TOKEN%"
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
