// https://chat.googleapis.com/v1/spaces/AAAAWH6z82U/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=0sqp1HU67GRDnTQpOCyuzLwvq53YJ9kyy_uiSDvfWlI
 
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
          post {
            success {
                def built_message = "seems like this step is working, successfully built."
                sendGoogleChatNotification(built_message)
            }
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
    