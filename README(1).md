# Containerized Flask Application on AWS

## Project Overview
This project demonstrates how to containerize a Python Flask application using Docker and deploy it on AWS using Amazon ECR, Amazon ECS, and AWS Fargate.

The Flask application was developed and tested locally using Docker. The Docker image was then pushed to Amazon ECR and deployed through Amazon ECS using AWS Fargate.

## Objective
To containerize a Python Flask application using Docker and deploy the containerized application on AWS.

## Technologies Used
- Python
- Flask
- Docker
- Amazon ECR
- Amazon ECS
- AWS Fargate
- AWS IAM
- Amazon VPC
- Security Groups

## Architecture

```text
Developer
   |
   v
Flask Application
   |
   v
Docker Image
   |
   v
Amazon ECR
   |
   v
Amazon ECS
   |
   v
AWS Fargate Task
   |
   v
Flask Docker Container
   |
   v
Port 5000
   |
   v
Web Browser
```

## Project Structure

```text
Containerized-Flask-Application/
|-- app.py
|-- requirements.txt
|-- Dockerfile
|-- README.md
`-- screenshots/
    |-- 01-flask-app-code.png
    |-- 02-dockerfile-requirements.png
    |-- 03-docker-image.png
    |-- 04-docker-container-local-test.png
    |-- 05-ecr-repository.png
    |-- 06-ecs-cluster.png
    |-- 07-ecs-running-task.png
    `-- 08-final-ecs-app.png
```

## Flask Application

The application displays:

```text
Hello from Flask Container on AWS ECS!
```

The application runs on port `5000`.

## Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

## Implementation Steps

### 1. Develop Flask Application
Created a basic Python Flask application.

### 2. Create Requirements File

```text
Flask
```

### 3. Build Docker Image

```bash
docker build -t flask-aws-app .
```

### 4. Run Container Locally

```bash
docker run -d -p 5000:5000 --name flask-aws-container flask-aws-app
```

Test:

```text
http://localhost:5000
```

Expected output:

```text
Hello from Flask Container on AWS ECS!
```

### 5. Create Amazon ECR Repository

Created an Amazon ECR repository named:

```text
flask-aws-app
```

### 6. Push Docker Image to ECR

```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.ap-south-1.amazonaws.com
```

```bash
docker tag flask-aws-app:latest <AWS_ACCOUNT_ID>.dkr.ecr.ap-south-1.amazonaws.com/flask-aws-app:latest
```

```bash
docker push <AWS_ACCOUNT_ID>.dkr.ecr.ap-south-1.amazonaws.com/flask-aws-app:latest
```

### 7. Create ECS Cluster

Created:

```text
flask-aws-cluster
```

### 8. Create ECS Task Definition

Created:

```text
flask-aws-task
```

Configuration:
- Launch type: Fargate
- OS: Linux
- Architecture: X86_64
- CPU: 1 vCPU
- Memory: 3 GB
- Container port: 5000

### 9. Create ECS Service

Created:

```text
flask-aws-service
```

### 10. Configure Security Group

Inbound rule:

```text
Protocol: TCP
Port: 5000
Source: 0.0.0.0/0
```

This was used for demonstration and testing.

### 11. Deploy Using AWS Fargate

ECS pulls the Docker image from Amazon ECR and AWS Fargate runs the Flask container without requiring EC2 server management.

## Final Result

The Flask application was successfully deployed on Amazon ECS using AWS Fargate.

Application endpoint:

```text
http://<PUBLIC-IP>:5000
```

Output:

```text
Hello from Flask Container on AWS ECS!
```

## Security

The project used IAM roles, VPC networking, Security Groups, and Amazon ECR.

For production, access to port 5000 should be restricted instead of allowing the entire internet.

## Project Limitation

The demonstration uses a single ECS task and direct public access. If the task stops, the application becomes unavailable until another task is running.

## Future Improvements

- Application Load Balancer
- Multiple ECS tasks
- ECS Service Auto Scaling
- HTTPS
- Restricted Security Groups
- CloudWatch monitoring
- AWS Secrets Manager
- CI/CD pipeline

## Key Learnings

- Docker containerization
- Flask application deployment
- Amazon ECR
- Amazon ECS
- AWS Fargate
- IAM roles
- VPC networking
- Security Groups
- Container deployment and testing

## TAR Project Summary

**Task:** Containerize and deploy a Flask application on AWS.

**Action:** Built and tested a Docker image, pushed it to Amazon ECR, deployed it using Amazon ECS Fargate, and configured IAM, networking, and Security Groups.

**Result:** Successfully deployed and tested the Flask application through a public ECS endpoint.

## Screenshots

Place these screenshots inside the `screenshots` folder:

1. `01-flask-app-code.png`
2. `02-dockerfile-requirements.png`
3. `03-docker-image.png`
4. `04-docker-container-local-test.png`
5. `05-ecr-repository.png`
6. `06-ecs-cluster.png`
7. `07-ecs-running-task.png`
8. `08-final-ecs-app.png`
