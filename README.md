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

## Step 3 - Amazon ECR Configuration

Amazon Elastic Container Registry (ECR) was used to store Docker images generated during the build process.

### ECR Repository Creation

The ECR repository was created to store Spring Boot Docker images.

![ECR Repository](screenshots/03-ecr/ECR.png)

### Updating ECR URI in buildspec.yml

The ECR repository URI was updated in the buildspec.yml file to ensure Docker images are pushed to the correct repository.

![ECR URI Update](screenshots/03-ecr/ecr-uri-update-1.png)

![ECR URI Update](screenshots/03-ecr/ecr-uri-update-2.png)

### Docker Push Commands

The buildspec.yml file was updated with Docker push commands.

![Docker Push Command](screenshots/03-ecr/docker-push-command-1.png)

![Docker Push Command](screenshots/03-ecr/docker-push-command-2.png)

## Step 4 - AWS CodeBuild Configuration

AWS CodeBuild was configured to automatically build the Spring Boot application and create Docker images.

### Build Project Creation

The CodeBuild project was configured with GitHub as the source provider.

![CodeBuild Project](screenshots/04-codebuild/codebuild-1.png)

### Initial Build Failure

During the first build attempt, an access permission issue was encountered.

![Build Failure](screenshots/04-codebuild/codebuild-access-denied.png)

### IAM Permission Fix

Additional permissions were granted to the CodeBuild IAM role.

![Permission Fix](screenshots/11-troubleshooting/codebuild-role-permission.png)

### Successful Build

After updating permissions and configuration, the build completed successfully.

![Build Success](screenshots/04-codebuild/Build-success.png)

### Additional Build Logs

![Build Log](screenshots/04-codebuild/codebuild-2.png)

![Build Log](screenshots/04-codebuild/codebuild-3.png)

![Build Log](screenshots/04-codebuild/codebuild-4.png)

![Build Log](screenshots/04-codebuild/codebuild-5.png)

![Build Log](screenshots/04-codebuild/codebuild-6.png)

![Build Log](screenshots/04-codebuild/codebuild-7.png)

![Build Log](screenshots/04-codebuild/codebuild-8.png)

![Build Log](screenshots/04-codebuild/codebuild-9.png)

![Build Log](screenshots/04-codebuild/codebuild-10.png)

![Build Log](screenshots/04-codebuild/codebuild-11.png)

![Build Log](screenshots/04-codebuild/codebuild-12.png)

![Build Log](screenshots/04-codebuild/codebuild-13.png)

![Build Log](screenshots/04-codebuild/codebuild-14.png)

### Build Retry

A manual retry was performed after fixing configuration issues.

![Retry Build](screenshots/04-codebuild/retry-build.png)

## Step 5 - Amazon ECS Cluster Creation

Amazon ECS Fargate was selected as the container orchestration platform.

### ECS Cluster Creation

An ECS cluster was created using the Fargate launch type.

![Cluster Creation](screenshots/05-ecs-cluster/ECS-cluster-creation-1.png)

![Cluster Creation](screenshots/05-ecs-cluster/ECS-cluster-creation-2.png)

## Step 6 - ECS Task Definition Creation

Task Definitions were created to define container configuration, CPU allocation, memory allocation, image URI, and networking requirements.

### Task Definition Configuration

![Task Definition](screenshots/06-task-definition/ECS-Task definition creation.png)

![Task Definition](screenshots/06-task-definition/ECS-Task definition creation-2.png)

### Task Definition Review

![Task Definition Review](screenshots/06-task-definition/Task definition-1.png)

![Task Definition Review](screenshots/06-task-definition/Task definition-3.png)

## Step 7 - ECS Service Creation

The ECS Service was created to manage and maintain running tasks.

### Service Creation

![Service Creation](screenshots/07-service/Create service-1.png)

![Service Creation](screenshots/07-service/Create service-2.png)

![Service Creation](screenshots/07-service/Create service-3.png)

![Service Creation](screenshots/07-service/Create service-4.png)

![Service Creation](screenshots/07-service/Create service-5.png)

### Deployment In Progress

The service deployment process was initiated and monitored.

![Deployment Progress](screenshots/07-service/ecs-service-deployment-progress.png)

## Step 8 - AWS CodePipeline Creation

AWS CodePipeline was configured to automate the entire CI/CD workflow.

### Pipeline Creation

![Pipeline Creation](screenshots/08-codepipeline/create-codepipeline.png)

![Pipeline Creation](screenshots/08-codepipeline/create-codepipeline-2.png)

![Pipeline Creation](screenshots/08-codepipeline/create-codepipeline-3.png)

![Pipeline Creation](screenshots/08-codepipeline/create-codepipeline-4.png)

![Pipeline Creation](screenshots/08-codepipeline/create-codepipeline-5.png)

![Pipeline Creation](screenshots/08-codepipeline/create-codepipeline-6.png)

![Pipeline Creation](screenshots/08-codepipeline/create-codepipeline-7.png)

### Source Stage

GitHub repository was configured as the source stage.

### Build Stage

AWS CodeBuild was configured as the build stage.

### Deploy Stage

Amazon ECS was configured as the deployment stage.

## Step 9 - Application Deployment

After successful pipeline execution, the application was automatically deployed to ECS Fargate.

### CodePipeline Deployment Success

![Pipeline Success](screenshots/09-deployment/codepipeline-deployment-success.png)

### Health Endpoint Verification

The Spring Boot Actuator endpoint confirmed the application was healthy.

![Health Check](screenshots/09-deployment/actuator-health-status-up.png)

Response:

{
  "status":"UP"
}

## Step 10 - Final Output

After deployment, the application became publicly accessible through the ECS public IP address.

### Successful Application Access

![Final Output](screenshots/10-output/Final Outcome-Success.png)

Output:

Welcome to Spring Boot AWS Deployment!


## Troubleshooting & Issues Resolved

Throughout the project several issues were encountered and successfully resolved.

### Issue 1 - CodeBuild Access Denied

CodeBuild initially failed because of insufficient IAM permissions.

![Access Denied](screenshots/11-troubleshooting/codebuild-access-denied.png)

### Issue 2 - IAM Role Permission Updates

Additional IAM policies were attached to the CodeBuild service role.

![IAM Role Update](screenshots/11-troubleshooting/attaching policy-codebuild IAM Role.png)

![IAM Role Update](screenshots/11-troubleshooting/permission-added-to codebuild -polici....png)

### Issue 3 - ECS Task Networking Issue

The ECS task initially failed due to networking configuration issues.

![Task Failure](screenshots/11-troubleshooting/ECS--cluster-task-clicked on task id-net....png)

### Issue 4 - Post Build Error

Build configuration errors were resolved by updating buildspec.yml and IAM permissions.

![Post Build Error](screenshots/11-troubleshooting/Post build error.png)

### Issue 5 - Docker Hub Rate Limit Issue

Docker Hub image pull limits caused build failures.

Resolution:
- Replaced Docker Hub base image.
- Used AWS-compatible image source.

![Docker Hub Issue](screenshots/11-troubleshooting/replace docker-hub image with AWS EC....png)

### Issue 6 - Application Returned 404 Error

The application initially returned a Spring Boot Whitelabel Error Page because no controller was mapped to the root path.

Resolution:
- Added HomeController.java
- Redeployed through CodePipeline

![Controller Fix](screenshots/11-troubleshooting/home-controller-pushed.png)

### CloudWatch Log Analysis

Application logs were reviewed through CloudWatch.

![CloudWatch Logs](screenshots/11-troubleshooting/cloudwatch-container-logs.png)


## Conclusion

This project demonstrates a complete AWS DevOps CI/CD implementation using:

- GitHub
- AWS CodePipeline
- AWS CodeBuild
- Amazon ECR
- Amazon ECS Fargate
- CloudWatch Logs
- Spring Boot
- Docker

The pipeline automatically builds, packages, containerizes, and deploys the application whenever code is pushed to GitHub, providing a fully automated deployment workflow.
