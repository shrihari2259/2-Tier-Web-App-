![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)



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
