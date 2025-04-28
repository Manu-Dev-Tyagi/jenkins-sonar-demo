pipeline {
    agent any

    tools {
        sonarQubeScanner 'sonar-scanner'
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
                    sh '''
                      sonar-scanner \
                      -Dsonar.projectKey=jenkins-sonar-demo \
                      -Dsonar.sources=. \
                      -Dsonar.host.url=http://localhost:9000
                    '''
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
