def gv 

pipeline {
  agent any
  
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
          input {
            message "Select the environment to deploy to"
            ok "Done"
            parameters { 
                choice(name: "ONE",choices: ["dev", "staging", "prod"], description: "Choose the version to build")
              choice(name: "TWO",choices: ["dev", "staging", "prod"], description: "Choose the version to build")

            }
          }
          steps  {
            script {
                gv.deployApp()
                echo " deploying into ${ONE}"
                echo " deploying into ${TWO}"

            }
          }
    }
  }
 
}
      
