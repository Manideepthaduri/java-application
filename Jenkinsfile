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

         stage('Docker Run') {
          agent { label 'Docker'}      
            steps{
                   script {
                sh 'docker run -d -p 8096:5000 --rm --name mani 961565152773.dkr.ecr.us-west-1.amazonaws.com/mani:latest'     
      }
    }
    
                }
            } 
            
      
      
    
