pipeline {
    environment{
        IMAGE_NAME="camille250/simple-java-app"
        
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
                sh "docker build - t ${iMAGE_NAME} :${BUILD_ID} ."
            }
        }  
        stage ("push to docker hub") {
            steps{
                withCredentials([usernamePassword(credentialId: "jenkins-dockerhub-cre", passwordVariable: "PASS",usernameVariable: "USER")]){
                    sh "echo $PASS |docker login -u $USER --password-stdin" 
                    sh "docker push ${IMAGE_NAME}:${BUILD_ID}"
                }
                         
            }
        }
    }
}