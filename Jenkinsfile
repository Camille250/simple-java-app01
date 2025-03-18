pipeline{
    environment{
        IMAGE_NAME="025600686378.dkr.ecr.us-east-2.amazonaws.com/simple-jave-app"
        
    }
    agent any
    tools{
        maven "Maven"
    }
    stages{
        stage ("testing stage") {
            steps{
                echo "No test for now"
            }
        }
        stage ("building stage") {
            steps{
                sh "mvn clean package"       
            }
        }  
        stage ("build and push to ECR") {
            steps{
                 steps{
                    sh "aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 025600686378.dkr.ecr.us-east-2.amazonaws.com"
                    sh "docker build -t ${IMAGE_NAME}:${BUILD_ID} ."
                    sh "docker push ${IMAGE_NAME}:${BUILD_ID}"
                }        
                         
            }
        }
    }
}