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
            steps {
                sh '''
              docker build . --tag mani:$BUILD_NUMBER
              docker tag mani:$BUILD_NUMBER 961565152773.dkr.ecr.us-west-1.amazonaws.com/mani:$BUILD_NUMBER

              '''
         }
         }
      
    stage('Run Docker container on Jenkins Agent') {
     agent { label 'Docker'}  
           steps {
   
                sh 'docker run -d -p 8080:8080 — name mani:${buildNumber}”'
 
            }
        }



     
                }
            } 
            
      
      
    
