pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Dhom-059/8.2CDevSecOps.git'
      }
    }
    stage('Install Dependencies') { steps { sh 'npm install' } }
    stage('Run Tests') { steps { sh 'npm test || true' } }
    stage('Generate Coverage Report') { steps { sh "npm run coverage || true" } }
    stage('NPM Audit (Security Scan)') { steps { sh 'npm audit || true' } }
    pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'npm audit --audit-level=critical || true'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                sh '''
                    npx @sonar/scan \
                      -Dsonar.token=5ebd69101a3f8b3854bdef14e8829782ae69d61 \
                      -Dsonar.projectKey=Dhom-059_8.2CDevSecOps \
                      -Dsonar.organization=dhom-059
                '''
            }
        }
    }
}

  }
}
