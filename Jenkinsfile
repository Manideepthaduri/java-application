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
              docker build . --tag web-application:$BUILD_NUMBER
              docker tag web-application:$BUILD_NUMBER 961565152773.dkr.ecr.us-west-1.amazonaws.com/mani:$BUILD_NUMBER

              '''
         }
         }
      
    stage('Push Docker Image') {
              steps {
                  withAWS(credentials: 'ECR', region: 'us-west-1') {
                   
                      sh '''
                   aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin 961565152773.dkr.ecr.us-west-1.amazonaws.com
                   docker push 961565152773.dkr.ecr.us-west-1.amazonaws.com/mani:$BUILD_NUMBER
                    '''
                }
            }

        
         stage(“Deploy docker image to the deployment server”){

           sshagent(['Docker']) {

            sh “ssh -o StrictHostKeyChecking=no ubuntu@54.193.122.230 docker rm -f todospringmongobackend || true”

             sh “ssh -o StrictHostKeyChecking=no ubuntu@54.193.122.230 docker run -d -p 8080:8080 — name todospringmongobackend imonbayazid/todo-spring-mongo-backend:${buildNumber}”

}

}





     
                }
            } 
            
      }
      
    
