pipeline {
    agent any
    tools{
        maven "Maven3.8.7"
    }
    stages {
      stage('Clone the repository'){
        steps{
          git 'https://github.com/Manideepthaduri/java-application.git'
          
        } 
      }
      
  stage('Build the code') {
            steps {
                sh 'mvn clean install'
            }
        }    
      
   stage('Build Docker Image') { 
       agent { label 'Docker'}
            steps {
                sh '''
              docker build . --tag mani:$BUILD_NUMBER
              docker tag mani:$BUILD_NUMBER 961565152773.dkr.ecr.us-west-1.amazonaws.com/mani:$BUILD_NUMBER

              '''
         }
         }

         stage('Push Docker Image') {
          steps{
 withAWS(credentials: 'ECR', region: 'us-west-1') {
       
                    sh '''
                   aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin 108290765801.dkr.ecr.us-west-1.amazonaws.com
                   docker push 108290765801.dkr.ecr.us-west-1.amazonaws.com/web-application:$BUILD_NUMBER
                    '''
                }
            } 
    
                }
            }
}
            
