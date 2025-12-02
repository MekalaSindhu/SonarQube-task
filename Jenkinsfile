pipeline {
    agent any

    environment {
        SONAR_AUTH_TOKEN = credentials('SONAR_AUTH_TOKEN')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/MekalaSindhu/SonarQube-task.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat """
                    "C:\\sonar-scanner\\bin\\sonar-scanner.bat" ^
                      -Dsonar.projectKey=SonarQube-task ^
                      -Dsonar.sources=.
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
