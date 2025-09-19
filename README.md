# AWS DevOps Portfolio Project

A Node.js application containerized with Docker and deployed to AWS EC2 with a fully automated CI/CD pipeline using GitHub Actions.

## Live Demo
http://13.60.89.129

## Architecture
GitHub (code) → GitHub Actions (CI/CD) → AWS EC2 (Docker container) → nginx (reverse proxy) → Port 80

## Tech Stack
- **App:** Node.js + Express
- **Container:** Docker (node:18-alpine)
- **Cloud:** AWS EC2 (t3.micro, Ubuntu 24.04)
- **CI/CD:** GitHub Actions
- **Web Server:** nginx (reverse proxy)
- **Networking:** AWS Security Groups

## CI/CD Pipeline
Every push to `main` automatically:
1. Builds a Docker image
2. Transfers the image to EC2 via SCP
3. Stops the old container
4. Starts the new container
5. App is live within ~2 minutes of pushing code

## Infrastructure Setup
- AWS IAM user with least-privilege permissions (EC2FullAccess only)
- EC2 Security Groups restricting traffic to ports 22, 80, 443, and 3000
- SSH key authentication (no password login)
- GitHub Actions secrets for secure credential storage (never in code)
- nginx reverse proxy routing port 80 traffic to the Node.js app on port 3000
- Docker container configured with `--restart unless-stopped` for automatic recovery on reboot

## API Endpoints
- `GET /` — returns app info and timestamp
- `GET /health` — health check endpoint

## What I Would Add Next
- HTTPS via Let's Encrypt SSL certificate
- nginx improvements
- Domain name via AWS Route 53
- Terraform
- AWS ECR
- CloudWatch 
- RDS Database
- Load balancer (ALB) 
- Kubernetes (EKS)
