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
 stage('Status Check'){
steps{
script{
withsonarqubeEnv('Sonarqube'){
        bat "C:/Users/bharg/Downloads/Maven/apache-maven-3.9.6/bin/mvn -X sonar:sonar"
}
            bat "C:/Users/bharg/Downloads/Maven/apache-maven-3.9.6/bin/mvn clean"

}
}

 
}}
}
//slackSend channel: '#mbandi-cloudformation-cicd', message: "Please find the pipeline status of the following ${env.JOB_NAME ${env.BUILD_NUMBER} ${env.BUILD_URL}"
