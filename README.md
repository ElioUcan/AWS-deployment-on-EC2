# AI Agent Deployment on AWS EC2

## 🛠️ Technologies
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Anthropic](https://img.shields.io/badge/Anthropic_API-191919?style=for-the-badge&logo=anthropic&logoColor=white)

## ✨ Features
- Deploy a multi-container FastAPI + PostgreSQL app to AWS EC2 with Docker Compose
- IAM user configured with a least-privilege custom policy (EC2 + S3 read only)
- Public HTTP endpoint on port 8000 served from Amazon Linux 2023
- SSH key pair access with a dedicated security group (`ai-agent-sg`)
- Secure environment variable handling — no secrets committed to Git

## 🎯 Uses
Takes the AI agent from local development to a real production cloud environment on AWS EC2. Covers the full deployment lifecycle: EC2 provisioning, Docker Compose in production, IAM configuration, and public API exposure. Built as project #5 in a Data/AI/MLOps engineering portfolio.

## 🔧 Process
Provisioned an EC2 `t3.micro` instance on Amazon Linux 2023, installed Docker and Docker Compose, configured a security group for ports 22 and 8000, set up an IAM deploy user with a minimal policy, and ran the multi-container app with Docker Compose. All sensitive values (API keys, DB credentials) are passed via a `.env` file that is never committed to Git.

## 💡 Learnings
- Running Docker Compose on EC2 requires installing Docker Buildx separately on Amazon Linux 2023 — it is not bundled by default
- IAM least-privilege means creating a dedicated deploy user with only the permissions it needs; the admin account is never used for automation
- Security groups are the first line of defense — only open the ports the app actually uses

## ▶️ Running the project

```bash
# Local setup
cp .env.example .env
docker-compose up -d

# AWS deployment — SSH into your EC2 instance, then:
git clone https://github.com/ElioUcan/AWS-deployment-on-EC2.git
cd AWS-deployment-on-EC2
cp .env.example .env  # fill in values
docker-compose up -d
```
