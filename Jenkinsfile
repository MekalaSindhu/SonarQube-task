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
                      -Dsonar.sources=. ^
                      -Dsonar.host.url=http://192.168.7.11:9000 ^
                      -Dsonar.token=%SONAR_AUTH_TOKEN1%
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
