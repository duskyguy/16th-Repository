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
        bat """C:/Build/apache-maven-3.9.8/bin/mvn -X sonar:sonar \
              -Dsonar.projectKey=JavaWebApp \
              -Dsonar.host.url=http:localhost:9000\
              -Dsonar.login=sqa_1fab6df7f1a4c6069f537d97f42f9e24aefc99dc"""
         // bat 'C:\Users\bharg\Downloads\sonarqube-developer-9.9.5.90363\sonarqube-9.9.5.90363\bin'
      }
    }
   
  }
}
//slackSend channel: '#mbandi-cloudformation-cicd', message: "Please find the pipeline status of the following ${env.JOB_NAME ${env.BUILD_NUMBER} ${env.BUILD_URL}"
