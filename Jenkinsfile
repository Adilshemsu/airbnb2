pipeline {
  agent any
 
  parameters {
    choice(name: "VERSION",choices: ["1.0.0", "1.0.1", "1.0.2"], description: "Choose the version to build")
    booleanParam(name: "DEPLOY", defaultValue: true, description: "Deploy the application")
  }
  stages{
    stage("build")  {
          steps  {
            echo "building the application.."
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
            
            
          }
    }
  }
 
}
      
