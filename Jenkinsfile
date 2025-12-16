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
            withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                bat '''
                C:\\sonar-scanner\\bin\\sonar-scanner.bat ^
                -Dsonar.projectKey=SonarQube-task ^
                -Dsonar.sources=. ^
                -Dsonar.token=%SONAR_TOKEN%
                '''
            }
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
