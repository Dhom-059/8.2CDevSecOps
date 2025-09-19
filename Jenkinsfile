pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Dhom-059/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    // keep tests/coverage optional for this assignment
    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('Security Scan') {
      steps {
        sh 'npm audit --audit-level=critical || true'
      }
    }

stage('SonarQube Analysis') {
  steps {
    withCredentials([string(credentialsId: 'sonarcloud-token', variable: 'SONAR_TOKEN')]) {
      sh '''
        npm install -g sonarqube-scanner
        sonar-scanner \
          -Dsonar.host.url=https://sonarcloud.io \
          -Dsonar.token=${SONAR_TOKEN} \
          -Dsonar.projectKey=Dhom-059_8.2CDevSecOps \
          -Dsonar.organization=dhom-059 \
          -Dsonar.sources=.
      '''
    }
  }
}

  }
}

