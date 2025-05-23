pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6' // Replace with the exact name configured in Jenkins
    }

    environment {
        SONAR_TOKEN = credentials('sonarcloud-token') // You must set this up in Jenkins > Credentials
    }

    stages {
        stage('Install Dependencies') {
            steps {
                bat 'echo Installing dependencies...'
                bat 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'echo Running tests...'
                bat 'mvn test'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    bat "mvn sonar:sonar -Dsonar.projectKey=YOUR_PROJECT_KEY -Dsonar.organization=YOUR_ORG_NAME -Dsonar.login=%SONAR_TOKEN%"
                }
            }
        }
    }
}
