# Project 8 – Containerized Flask Application on AWS ECS

## 1. Project Overview

This project demonstrates how to containerize a Python Flask application using Docker and deploy the containerized application on AWS using Amazon ECR and Amazon ECS.

The Flask application is first developed and tested locally. A Docker image is then created and pushed to Amazon ECR. Amazon ECS with AWS Fargate is used to run the Docker container.

The final application can be accessed through the public IP address of the running ECS task.

---

## 2. Objective

The objective of this project is to:

- Develop a basic Python Flask application.
- Create a Dockerfile for the Flask application.
- Build a Docker image.
- Test the Docker container locally.
- Create an Amazon ECR repository.
- Push the Docker image to ECR.
- Create an Amazon ECS cluster.
- Create an ECS task definition.
- Deploy the application using ECS Fargate.
- Access and test the running Flask application.

---

## 3. AWS Services and Technologies Used

| Service / Technology | Purpose |
|---|---|
| Python Flask | Application framework |
| Docker | Containerize the Flask application |
| Amazon ECR | Store the Docker image |
| Amazon ECS | Run and manage the container |
| AWS Fargate | Serverless compute for the ECS task |
| IAM | Provide required permissions |
| Amazon VPC | Provide networking for the ECS task |
| Security Group | Control network access to port 5000 |

The project requirements specify Flask, Docker, Amazon ECR and Amazon ECS as the main technologies/services for this implementation.

---

## 4. Application

The Flask application provides a simple web page.

### Application Response

```text
Hello from Flask Container on AWS ECS!