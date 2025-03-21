pipeline {
    environment {
        ACCOUNT_ID = "585443148081.dkr.ecr.us-east-1.amazonaws.com"
        REPO_NAME = "simple-java-app2"
        AWS_REGION = "us-east-1"
        IMAGE_NAME = "${ACCOUNT_ID}/${REPO_NAME}"
    }
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage("Testing Stage") {
            steps {
                echo "No test for now"
            }
        }
        stage("Building Stage") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Build Docker Image") {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${BUILD_ID} ."
                }
            }
        }
        stage("Push to ECR") {
            steps {
                withCredentials([aws(credentialsId: 'aws-credentials', region: 'us-east-1')]) {
                    sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${ACCOUNT_ID}"
                    sh "docker push ${IMAGE_NAME}:${BUILD_ID}"
                }
            }
        }
    }
}