pipeline {
  agent any

  environment {
    GOOGLE_CHAT_WEBHOOK = credentials ('google-chat-webhook-trial')
  }

  stages {
      stage('Build') {
          steps {
              echo "Building the project..."
          }
      }

      stage('Test') {
          steps {
              echo "Running tests..."
          }
      }

      stage('Deploy') {
          steps {
              echo "Deploying the application..."
          }
      }
  }

  post {
    success {
        script {
            def message = "✅ *Build Successful!* 🚀\n*Job:* ${env.JOB_NAME} #${env.BUILD_NUMBER}\n*URL:* ${env.BUILD_URL}"
            sendGoogleChatNotification(message)
        }
    }
    failure {
        script {
            def message = "❌ *Build Failed!* 🔥\n*Job:* ${env.JOB_NAME} #${env.BUILD_NUMBER}\n*URL:* ${env.BUILD_URL}"
            sendGoogleChatNotification(message)
        }
    }
  }
}

def sendGoogleChatNotification(String message) {
    sh """
        curl -X POST -H "Content-Type: application/json" \
        -d '{"text": "'"${message//\"/\\\"}"'"}' \
        "$GOOGLE_CHAT_WEBHOOK"
    """
}
