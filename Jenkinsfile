pipeline{
    environment{
        IMAGE_NAME="${ACCOUNT_ID}/${REPO_NAME}:${BUILD_ID}"
        ACCOUNT_ID="585443148081.dkr.ecr.us-east-1.amazonaws.com"
        AWS_REGION="us-east-1"
        REPO_NAME="simple-java-app2"        
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
        stage ("build docker image") {
            steps{
                script{
                    docker.build("${IMAGE_NAME}")
                }

            }
        }    
        stage ("push to ECR") {
            steps{
                 script{
                    docker.withRegistry("https://${ACCOUNT_ID}", "ecr:${AWS_REGION}:aws-credentials"){
                        docker.push("${BUILD_ID}")
                    }
                }        
                         
            }
        }
    }
}