pipeline{
    agent any
    
    environment {
        CR_PAT= "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"
    }
    
    stages{
        stage("Clone Code"){
            steps{
                echo "Cloning the code"
                git url: "https://github.com/Ashish8800/classs.git/", branch: "main"
            }
            
        }
        stage("build"){
            steps{
                echo "Building the Image"
                sh "docker build -t my-node-app ."
                sh "docker tag my-node-app ghcr.io/ashish8800/node:latest"
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                echo "Pushing the Image"
                sh "export CR_PAT=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"
                sh "echo ${CR_PAT} | docker login ghcr.io -u ashish8800 --password-stdin "
                sh " docker push ghcr.io/ashish8800/node"
                
            }
            
        }
        stage("Deploy"){
            steps{
                echo "Deploying the Container"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
