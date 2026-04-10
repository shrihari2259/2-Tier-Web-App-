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
⚠️ IMPORTANT (YOU MUST CHANGE)

Replace:

YOUR-REPO.git
172.31.x.x
☸️ 4. CONVERT TO KUBERNETES (PRO LEVEL 🚀)

Now we upgrade your project to Kubernetes.

📄 1. flask-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: flask-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: flask
  template:
    metadata:
      labels:
        app: flask
    spec:
      containers:
      - name: flask
        image: your-docker-image
        ports:
        - containerPort: 5000
        env:
        - name: MYSQL_HOST
          value: "mysql-service"
        - name: MYSQL_USER
          value: "admin"
        - name: MYSQL_PASSWORD
          value: "admin123"
        - name: MYSQL_DB
          value: "testdb"
🌐 2. flask-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: flask-service
spec:
  type: LoadBalancer
  selector:
    app: flask
  ports:
    - port: 80
      targetPort: 5000
🐬 3. mysql-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        env:
        - name: MYSQL_ROOT_PASSWORD
          value: "root"
        - name: MYSQL_DATABASE
          value: "testdb"
        ports:
        - containerPort: 3306
🌐 4. mysql-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
spec:
  ports:
    - port: 3306
  selector:
    app: mysql
    
🚀 HOW TO RUN K8s
kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml
kubectl apply -f flask-deployment.yaml
kubectl apply -f flask-service.yaml
💥 FINAL RESULT (WHAT YOU NOW HAVE)

