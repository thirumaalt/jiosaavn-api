pipeline {
  agent any

  environment {
    IMAGE_NAME = "jiosaavn-api-local"
    CONTAINER_NAME = "jiosaavn-api-container"
  }

  stages {
    stage('Clone Repository') {
      steps {
        git branch: 'main', 
            url: 'https://github.com/thirumaalt/jiosaavn-api.git', 
            credentialsId: 'Git_Token'
      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          sh "docker build -t $IMAGE_NAME ."
        }
      }
    }

    stage('Stop Existing Container') {
      steps {
        script {
          sh "docker rm -f $CONTAINER_NAME || true"
        }
      }
    }

    stage('Run Docker Container Locally') {
      steps {
        script {
          sh "docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME"
        }
      }
    }
  }

  post {
    success {
      echo "✅ JioSaavn API is now running at http://localhost:3000"
    }
    failure {
      echo "❌ Something went wrong."
    }
  }
}
