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
    stage('Build') {
      steps {
         bat 'C:/Users/bharg/Downloads/Maven/apache-maven-3.9.6/bin/mvn clean'
 
      }
      post {
        success {
          echo ' now Archiving '
         // archiveArtifacts artifacts: '**/*.war'
        }
      }
    }
    stage('Unit Test'){
        steps {
         bat 'C:/Users/bharg/Downloads/Maven/apache-maven-3.9.6/bin/mvn test'
        }
    }
    stage('Integration Test'){
        steps {
         // sh 'mvn verify -DskipUnitTests'
                     bat 'C:/Users/bharg/Downloads/Maven/apache-maven-3.9.6/bin/mvn verify -DskipUnitTests'

        }
    }
    stage ('Checkstyle Code Analysis'){
        steps {
           // sh 'mvn checkstyle:checkstyle'
                    bat 'C:/Users/bharg/Downloads/Maven/apache-maven-3.9.6/bin/mvn checkstyle:checkstyle'

        }
        post {
            success {
                echo 'Generated Analysis Result'
            }
        }
    }
    stage('SonarQube Scan') {
      steps {
       // sh """mvn sonar:sonar \
             // -Dsonar.projectKey=JavaWebApp \
             // -Dsonar.host.url=http://172.31.4.143:9000 \
            //  -Dsonar.login=e9733df3fcd6ed54cef307d8ac4cc00eeb2d3611"""
          bat 'C:\Users\bharg\Downloads\sonarqube-developer-9.9.5.90363\sonarqube-9.9.5.90363\bin'
      }
    }
    stage('Upload to Artifactory') {
      steps {
        sh "mvn clean deploy -DskipTests"
      }
    }
    stage('Deploy to DEV') {
      environment {
        HOSTS = "dev"
      }
      steps {
        sh "ansible-playbook ${WORKSPACE}/deploy.yaml --extra-vars \"hosts=$HOSTS workspace_path=$WORKSPACE\""
      }
     }
    // stage('Approval for stage') {
    //   steps {
    //     input('Do you want to proceed?')
    //   }
    // }
    stage('Deploy to Stage') {
      environment {
        HOSTS = "stage" // Make sure to update to "stage"
      }
      steps {
        sh "ansible-playbook ${WORKSPACE}/deploy.yaml --extra-vars \"hosts=$HOSTS workspace_path=$WORKSPACE\""
      }
    }
    stage('Approval') {
      steps {
        input('Do you want to proceed?')
      }
    }
    stage('Deploy to PROD') {
      environment {
        HOSTS = "prod"
      }
      steps {
        sh "ansible-playbook ${WORKSPACE}/deploy.yaml --extra-vars \"hosts=$HOSTS workspace_path=$WORKSPACE\""
      }
    }
  }
  post {
    always {
        echo 'Slack Notifications.'
        slackSend channel: '#mbandi-jenkins-cicd-pipeline-alerts', //update and provide your channel name
        color: COLOR_MAP[currentBuild.currentResult],
        message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
    }
  }
}

//slackSend channel: '#mbandi-cloudformation-cicd', message: "Please find the pipeline status of the following ${env.JOB_NAME ${env.BUILD_NUMBER} ${env.BUILD_URL}"
