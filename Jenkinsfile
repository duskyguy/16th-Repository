def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]
pipeline {
  agent any
  environment {
    WORKSPACE = "${env.WORKSPACE}"
  }
 
  stages {
   
    stage('SonarQube Scan') {
      steps {
        bat """mvn sonar:sonar \
              -Dsonar.projectKey=JavaWebApp \
              -Dsonar.host.url=http:localhost:9000 \
              -Dsonar.login=26684937d2214b3438509d6c4fd35697fdd312ce"""
         // bat 'C:\Users\bharg\Downloads\sonarqube-developer-9.9.5.90363\sonarqube-9.9.5.90363\bin'
      }
    }
   
  }
 
}

//slackSend channel: '#mbandi-cloudformation-cicd', message: "Please find the pipeline status of the following ${env.JOB_NAME ${env.BUILD_NUMBER} ${env.BUILD_URL}"
