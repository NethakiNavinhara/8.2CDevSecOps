pipeline {
  agent any

  environment {
    SONAR_TOKEN = credentials('SONAR_TOKEN')
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/NethakiNavinhara/8.2CDevSecOps.git', branch: 'main'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'npm test || exit 0'
      }
    }

    stage('SonarCloud Analysis') {
      steps {
        withEnv(["SONAR_TOKEN=${env.SONAR_TOKEN}"]) {
          bat """
            npx sonar-scanner ^
              -Dsonar.projectKey=NethakiNavinhara_8.2CDevSecOps ^
              -Dsonar.organization=nethakinavinhara ^
              -Dsonar.sources=. ^
              -Dsonar.host.url=https://sonarcloud.io ^
              -Dsonar.login=%SONAR_TOKEN%
          """
        }
      }
    }
  }
}
