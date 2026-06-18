# AWS DevOps Spring Boot Application Deployment using ECS Fargate

## Project Overview

This project demonstrates an end-to-end CI/CD pipeline for deploying a Spring Boot application using AWS services.

The deployment workflow is:

GitHub → CodePipeline → CodeBuild → Amazon ECR → Amazon ECS Fargate

Whenever code is pushed to GitHub, the pipeline automatically:

- Downloads source code
- Builds the application using Maven
- Creates a Docker image
- Pushes the image to Amazon ECR
- Deploys the latest image to Amazon ECS Fargate

## Technologies Used

- Java 17
- Spring Boot
- Maven
- Docker
- GitHub
- AWS CodeBuild
- AWS CodePipeline
- Amazon ECR
- Amazon ECS Fargate
- CloudWatch Logs

## Architecture

GitHub
    ↓
CodePipeline
    ↓
CodeBuild
    ↓
Amazon ECR
    ↓
Amazon ECS Fargate
    ↓
Spring Boot Application

## Repository Structure

aws-devops-springbootapp
│
├── src
├── src
│   ├── main
│   └── test
│
├── screenshots
│   ├── 01-source-code
│   ├── 02-github
│   ├── 03-ecr
│   ├── 04-codebuild
│   ├── 05-ecs-cluster
│   ├── 06-task-definition
│   ├── 07-service
│   ├── 08-codepipeline
│   ├── 09-deployment
│   ├── 10-output
│   └── 11-troubleshooting
│
├── Dockerfile
├── buildspec.yml
├── pom.xml
└── README.md
