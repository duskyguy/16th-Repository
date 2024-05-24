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
        sh """mvn sonar:sonar \
              -Dsonar.projectKey=JavaWebApp \
              -Dsonar.host.url=http://172.31.4.143:9000 \
              -Dsonar.login=e9733df3fcd6ed54cef307d8ac4cc00eeb2d3611"""
         // bat 'C:\Users\bharg\Downloads\sonarqube-developer-9.9.5.90363\sonarqube-9.9.5.90363\bin'
      }
    }
   
  }
 
}

//slackSend channel: '#mbandi-cloudformation-cicd', message: "Please find the pipeline status of the following ${env.JOB_NAME ${env.BUILD_NUMBER} ${env.BUILD_URL}"
