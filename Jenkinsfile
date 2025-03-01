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
                script {
                def built_message = "seems like this step is working, successfully built."
                GoogleChatNotification(built_message)
                }
            }
            failure {
                script {
                    def failure_message = "something fucked up."
                    GoogleChatNotification(failure_message)
                }
            }
          }
      }

      stage('Test') {
          steps {
              echo "Running tests..."
          }
          post {
            success {
                script {
                    def test_message = "test stage works."
                    GoogleChatNotification(test_message)
                }
            }
            failure {
                script {
                    def failure_message = "something fucked up."
                    GoogleChatNotification(failure_message)
                }
            }
          }
      }

      stage('Deploy') {
          steps {
              echo "Deploying the application..."
          }
          post {
            success {
                script {
                    def deploy_message = "its deployed bitch"
                    GoogleChatNotification(deploy_message)
                }
            }
            failure {
                script {
                    def failure_message = "something fucked up."
                    GoogleChatNotification(failure_message)
                }
            }
          }
      }
  }

  post {
    success {
        script {
            def message = "✅ *Build Successful!* 🚀\n*Job:* ${env.JOB_NAME} #${env.BUILD_NUMBER}\n*URL:* ${env.BUILD_URL}"
            GoogleChatNotification(message)
        }
    }
    failure {
        script {
            def message = "❌ *Build Failed!* 🔥\n*Job:* ${env.JOB_NAME} #${env.BUILD_NUMBER}\n*URL:* ${env.BUILD_URL}"
            GoogleChatNotification(message)
        }
    }
  }
}

// def sendGoogleChatNotification(message) {
//     def url = env.GOOGLE_CHAT_WEBHOOK
//     def payload = [
//         text: message
//     ]
//     def response = httpRequest(
//         contentType: 'APPLICATION_JSON',
//         httpMode: 'POST',
//         requestBody: groovy.json.JsonOutput.toJson(payload),
//         url: url
//     )
//     if (response.status != 200) {
//         error "Failed to send message to Google Chat. HTTP status: ${response.status}, Response: ${response.content}"
//     }
// }
    
def GoogleChatNotification(message){
    def url = env.GOOGLE_CHAT_WEBHOOK
    def payload = [
        text: message
    ]
}