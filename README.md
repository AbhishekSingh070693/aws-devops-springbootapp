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

## Step 1 - Source Code Preparation

The Spring Boot application source code was prepared before creating the CI/CD pipeline.

### Project Structure

![Project Structure](screenshots/01-source-code/springboot-project-structure.png)

### Maven Configuration

The pom.xml file contains all required dependencies for the Spring Boot application.

![POM File](screenshots/01-source-code/pom.xml.png)

### Dockerfile

The Dockerfile is used by AWS CodeBuild to create the Docker image that will later be pushed to Amazon ECR.

![Dockerfile](screenshots/01-source-code/dockerfile.png)

### Home Controller

A HomeController was added to handle requests to the root URL (/). Without this controller, the application displayed a 404 Whitelabel Error Page.

```java
@RestController
public class HomeController {

    @GetMapping("/")
    public String home() {
        return "Welcome to Spring Boot AWS Deployment!";
    }
}
```

![Home Controller](screenshots/01-source-code/home-controller.png)


## Step 2 - GitHub Repository Setup

The source code was pushed to GitHub and used as the source stage for AWS CodePipeline.

![GitHub Repository](screenshots/02-github/Repository-forked.png)
