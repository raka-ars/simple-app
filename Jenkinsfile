pipeline {
  agent any

  environment {
    IMAGE_NAME = 'rakaganteng/simple-app'
    REGISTRY_CREDENTIALS = 'dockerhub-credentials'
  }

  stages {

    stage('Checkout') {
      steps {
        echo '📦 Checkout source code dari GitHub...'
        checkout scm
      }
    }

    stage('Build Info') {
      steps {
        bat 'echo "Mulai proses build pipeline (Windows Host + Docker Only)"'
        bat 'docker --version'
      }
    }

    stage('Build Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: env.REGISTRY_CREDENTIALS, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          bat """
            echo 🔑 Login ke Docker Hub...
            docker login -u %USER% -p %PASS%

            echo 🏗️  Membuat image Docker...
            docker build -t ${env.IMAGE_NAME}:${env.BUILD_NUMBER} .

            echo 🚪 Logout dari Docker Hub...
            docker logout
