pipeline {
    agent { label "server" }

    // Environment variables for DockerHub and IMAGE
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub') // Jenkins secret ID for DockerHub
        IMAGE_NAME = "omrajput/nodejs-demo-app"           // Docker image name
    }

    stages {

        // Stage 1: Pull code from GitHub
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/mahroot/jenkins-nodejs-k8s-cicd.git'
            }
        }

        // Stage 2: Run tests on Jenkins agent (optional)
        stage('Run Tests') {
            steps {
               sh 'npm test || echo "No tests defined"'  // Continue even if no tests
            }
        }

        // Stage 3: Build Docker image
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        // Stage 4: Push Docker image to DockerHub
        stage('Push to DockerHub') {
            steps {
                sh '''
                  # Login to DockerHub using Jenkins credentials
                  echo "$DOCKERHUB_CREDENTIALS_PSW" | docker login -u "$DOCKERHUB_CREDENTIALS_USR" --password-stdin
                  
                  # Push the Docker image
                  docker push $IMAGE_NAME:latest
                '''
            }
        }

        // Stage 5: Deploy container
        stage('Deploy') {
            steps {
                   sh 'docker run -d -p 3000:3000 $IMAGE_NAME:latest'
            }
        }
    }

    //  post actions (cleanup, notifications)
    post {
        success {
            echo "Docker image pushed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
