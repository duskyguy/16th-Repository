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
        bat """C:/Users/bharg/Downloads/Maven/apache-maven-3.9.6/bin/mvn -X sonar:sonar \
              -Dsonar.projectKey=JavaWebApp \
              -Dsonar.host.url=http:localhost:9000\
              -Dsonar.login=squ_2414e61c504101657677f56fd19799ba702dcb78"""
         // bat 'C:\Users\bharg\Downloads\sonarqube-developer-9.9.5.90363\sonarqube-9.9.5.90363\bin'
      }
    }
   
  }
}
//slackSend channel: '#mbandi-cloudformation-cicd', message: "Please find the pipeline status of the following ${env.JOB_NAME ${env.BUILD_NUMBER} ${env.BUILD_URL}"
