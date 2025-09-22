Node.js CI/CD Pipeline with Jenkins & Docker

Project Overview
This project demonstrates how to set up a **CI/CD pipeline** for a simple Node.js application using:
Jenkins → Automation server for CI/CD
Docker → Containerization of the Node.js app
DockerHub → Image registry to store and share Docker images
GitHub → Source code repository

CI/CD Workflow
1. Code pushed to GitHub → Jenkins job is triggered.  
2. Jenkins clones the repo and installs Node.js dependencies.  
3. Jenkins runs tests (if defined).  
4. Jenkins builds a Docker image of the app.  
5. Jenkins pushes the image to DockerHub.  
6. The container can be run locally or on a server.  

Docker Usage
 Build Image Locally
docker build -t omrajput/nodejs-demo-app:latest .

Pull from DockerHub
docker pull omrajput/nodejs-demo-app:latest

Run Container
docker run -p 3000:3000 omrajput/nodejs-demo-app:latest

Access app at: http://localhost:3000

