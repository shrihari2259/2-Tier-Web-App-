![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)


🏗️ 2. ARCHITECTURE DIAGRAM (IMAGE)
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
