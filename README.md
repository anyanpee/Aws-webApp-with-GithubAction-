# 🚀 Deploying a Scalable AWS 3-Tier Web App Using Terraform, Ansible, Docker, and GitHub Actions

## 🧠 Project Overview
This project automates the provisioning and deployment of a containerized Flask application (Monty Hall Game) on AWS using Terraform, Docker, Ansible, and GitHub Actions. The architecture is built for scalability, modularity, and production-readiness — following a true DevOps lifecycle approach.

## 📁 Project Architecture

![Architecture](./assets/AWS-Three-Tier-Architecture.jpg)

### Breakdown:
- **VPC**: Custom VPC with private and public subnets across 2 AZs  
- **EC2**: 1 Bastion Host (public), 2 App Instances (private)  
- **ALB**: Load balances across app servers  
- **RDS** (optional): PostgreSQL instance in private subnet  
- **ECR**: Stores Docker image  
- **S3 & DynamoDB**: Remote Terraform backend with state locking  
- **IAM**: Scoped roles for Terraform, EC2, ECR access  
- **Ansible**: Used for EC2 post-provision configuration and Docker deployment

---

## Technologies Used

| Tool               | Purpose                                                                 |
|--------------------|-------------------------------------------------------------------------|
| **Terraform**      | Infrastructure as Code to provision all AWS resources                  |
| **Ansible**        | Configure EC2 instances, install Docker, pull image, run container     |
| **Docker**         | Containerize the Flask app                                              |
| **GitHub Actions** | CI/CD automation for Terraform apply/destroy, and app deployment       |
| **Amazon ECR**     | Store and pull Docker images securely                                  |
| **Application Load Balancer** | Evenly distribute traffic across app instances              |

---

##  CI/CD Pipeline Workflow

The GitHub Actions pipeline performs the following jobs:

- **Terraform Init & Plan** — Validate infrastructure setup  
- **Terraform Apply/Destroy** — Build or destroy AWS resources  
- **Provisioning** — Use Ansible to configure EC2 and deploy Docker app  
- **Image Build & Push** — Build Flask app into Docker image and push to ECR  
- **Deploy to EC2** — Pull image and run container on EC2

---

##  Secrets Configuration (GitHub)

You’ll need to add the following secrets to your GitHub repository:

```yaml
AWS_ACCESS_KEY_ID: <your-access-key>
AWS_SECRET_ACCESS_KEY: <your-secret-key>
EC2_PRIVATE_SSH_KEY: <your-private-key>
EC2_PUBLIC_SSH_KEY: <your-public-key>

ssh-keygen -t rsa -b 4096 -f ~/.ssh/aws_key
chmod 400 ~/.ssh/aws_key

Paste the keys into GitHub repo settings > Secrets and variables > Actions.

 How to Use

    Fork or clone the repo

    Set your secrets in GitHub Actions

    Trigger the workflow from the Actions tab

    After deployment, visit your ALB DNS to access the app

    Tear down when done to avoid AWS billing

 Contributions & Improvements by Me

    Migrated provisioning from raw Bash to Ansible

    Improved container handling: ensures port 80 is freed before deploy

    Added idempotency with checks on running containers before redeploy

    Simplified Docker image pull and run logic with ECR login in pipeline

    Automated full CI/CD lifecycle via GitHub Actions with clear trigger stages

To-Do / Enhancements

Ansible integration for EC2 configuration

Add monitoring with CloudWatch or Prometheus

Add DNS integration using Route53

    Integrate Slack notifications via Lambda

Resources

    AWS Terraform Modules

    Ansible Docs

    GitHub Actions

    ECR Authentication

Author

Anyankpele Peter
DevOps Engineer with 5+ years in AWS, automation, and scalable deployments.
LinkedIn Profile - https://www.linkedin.com/in/peter-anyankpele

If this project helped or inspired you, feel free to star it. Fork it, expand it, and build something awesome!