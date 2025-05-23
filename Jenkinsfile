pipeline {
    agent any

    tools {
        nodejs "NodeJS"  // Optional: use if your Jenkins has NodeJS configured
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token-id') // Configure in Jenkins > Credentials
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh 'npx sonar-scanner'
                }
            }
        }
    }
}
