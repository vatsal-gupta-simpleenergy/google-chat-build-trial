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

def sendGoogleChatNotification(message) {
    def url = env.GOOGLE_CHAT_WEBHOOK
    def payload = [
        text: message
    ]
    def response = httpRequest(
        contentType: 'APPLICATION_JSON',
        httpMode: 'POST',
        requestBody: groovy.json.JsonOutput.toJson(payload),
        url: url
    )
    if (response.status != 200) {
        error "Failed to send message to Google Chat. HTTP status: ${response.status}, Response: ${response.content}"
    }
}
