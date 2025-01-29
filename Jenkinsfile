def gv 

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
    stage("init")  {
          steps  {
            script {
                gv = load "script.groovy"
            }
          }
    }
    stage("build")  {
          steps  {
            script {
                gv.buildApp()
            }
          }
    }
    stage("test")  {

        when {
            expression {
                return params.DEPLOY
            }
        } 
          steps  {
            script {
                gv.testApp()
            }
          }
    }
    stage("deploy")  {
          steps  {
            script {
                gv.deployApp()
            }
          }
    }
  }
 
}
      
