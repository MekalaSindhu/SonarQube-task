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
                    bat '''
                    sonar-scanner \
                      -Dsonar.projectKey=SonarQube-demo \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://192.168.0.100:9000 \
                      -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
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
