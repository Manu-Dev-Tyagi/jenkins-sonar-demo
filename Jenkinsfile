pipeline {
    agent any

    tools {
        sonarQubeScanner 'DefaultScanner'
    }

    environment {
        SONARQUBE = credentials('sonar-token')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Manu-Dev-Tyagi/jenkins-sonar-demo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('LocalSonarQube') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
