![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

🚀 About This Project

This project is a fully containerized Two-Tier Web Application built using Flask (Python) and MySQL, designed and deployed using modern DevOps practices on AWS EC2. It demonstrates the complete lifecycle of a real-world application from development to deployment using CI/CD automation, containerization, and cloud infrastructure management.

The application follows a microservice-style architecture, where the frontend/backend logic (Flask application) interacts with a separate MySQL database service. The entire system is containerized using Docker, ensuring portability, scalability, and consistency across environments.

To automate deployment, a Jenkins CI/CD pipeline is integrated, which pulls code from GitHub, builds a Docker image, and deploys the application on an AWS EC2 instance. This eliminates manual deployment steps and enables continuous delivery.

Additionally, the project is designed to be production-ready with support for:

Environment-based configuration
Docker networking for service communication
Reverse proxy support using Nginx (optional enhancement)
Monitoring integration using Prometheus & Grafana (advanced setup)
Infrastructure automation using Terraform (optional extension)
🎯 Key Highlights
Two-tier architecture (Flask + MySQL)
Fully containerized using Docker
CI/CD automation using Jenkins
Cloud deployment on AWS EC2
Environment variable-based configuration
Scalable and portable design
Production-style DevOps workflow
🧠 Problem Solved

Traditional deployments require manual setup of servers, dependencies, and configurations. This project solves that by:

Automating build and deployment processes
Eliminating environment inconsistency issues
Simplifying application scaling and portability
Reducing deployment time using CI/CD pipelines
⚙️ Outcome

This project demonstrates a real-world DevOps workflow where code changes automatically flow from GitHub → Jenkins → Docker → AWS EC2, resulting in a fully deployed application with minimal manual intervention.

🏆 Ideal For
DevOps Engineering portfolios
Cloud & DevOps internships
Resume project showcasing
CI/CD and Docker learning demonstration

🏗️ 2. ARCHITECTURE DIAGRAM (IMAGE)
📌 Simple Professional Diagram

You can use this in README:

                ┌──────────────┐
                │   GitHub     │
                └─────┬────────┘
                      │
                      ▼
               ┌──────────────┐
               │   Jenkins    │
               └─────┬────────┘
                     │
                     ▼
              ┌───────────────┐
              │  Docker Build │
              └─────┬─────────┘
                    │
         ┌──────────┴──────────┐
         ▼                     ▼
 ┌──────────────┐     ┌──────────────┐
 │ Flask App    │     │  MySQL DB    │
 │ Container    │     │ Container    │
 └──────────────┘     └──────────────┘
         │
         ▼
   AWS EC2 Deployment
🎯 If you want IMAGE version (better)

Tell me and I’ll generate a downloadable PNG architecture diagram for GitHub ⭐

🔥 3. JENKINSFILE (FULL CI/CD PIPELINE)

Create file:

Jenkinsfile

Paste this:

pipeline {
    agent any

    environment {
        IMAGE_NAME = "two-tier-flask-app"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/YOUR-REPO.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop flask-app || true
                docker rm flask-app || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d -p 5000:5000 \
                --name flask-app \
                -e MYSQL_HOST=172.31.x.x \
                -e MYSQL_USER=admin \
                -e MYSQL_PASSWORD=admin123 \
                -e MYSQL_DB=testdb \
                $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful 🚀'
        }
        failure {
            echo 'Deployment Failed ❌'
        }
    }
}
