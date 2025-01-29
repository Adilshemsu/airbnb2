pipeline {
  agent any
  environment {
        NEW_VERSION = "1.0.0"
        SERVER_CREDENTIALS = credentials('server-credentials')
  }
  tools {
    maven 'maven'
  }
  parameters {
    choice(name: "VERSION",choices: ["1.0.0", "1.0.1", "1.0.2"], description: "Choose the version to build")
    booleanParam(name: "DEPLOY", defaultValue: true, description: "Deploy the application")
  }
  stages{
    stage("build")  {
          steps  {
            echo "building the application.."
            echo "building version ${NEW_VERSION}"
          }
    }
    stage("test")  {

        when {
            expression {
                return params.DEPLOY
            }
        }
          steps  {
            echo "testing the application.."
          }
    }
    stage("deploy")  {
          steps  {
            echo "deploying the application .."
            echo "Deploying version ${params.VERSION}"
            echo "Deploying with ${SERVER_CREDENTIALS}"
            sh "${SERVER_CREDENTIALS}"
            withCredentials([usernamePassword(credentialsId: 'server-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
              sh "echo $USERNAME"
              sh "echo $PASSWORD"
            }
          }
    }
  }
 
}
      
