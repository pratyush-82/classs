pipeline{
    agent any
    
    environment {
        GITHUB_TOKEN= credentials('github-token')
    }
    
    stages{
        stage("Clone Code"){
            steps{
                echo "Cloning the code"
                git url: "https://github.com/Ashish8800/classs.git/", branch: "main"
            }
            
        }
        stage("building the code"){
            steps{
                echo "Building the Image"
                sh "cd ${WORKSPACE} && docker build -t my-node-app ."
                sh "docker tag my-node-app ghcr.io/ashish8800/node:latest"
            }
            
        }
        stage("Push to Docker Hub"){
            steps{
                echo "Pushing the Image"
                sh "export CR_PAT=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"
                sh "echo $GITHUB_TOKEN_PSW | docker login ghcr.io -u $GITHUB_TOKEN_USR --password-stdin"
                sh "docker push ghcr.io/ashish8800/node"
                
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
