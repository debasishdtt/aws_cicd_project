<h1 align="center" id="title">Microservice Project: Emart-app</h1>

## Introduction
<p>The project is about focusing on integrating AWS services to construct a robust CI/CD pipeline entirely within the AWS environment.</p>

<h5>🌟About</h5>
This project was developed as part of a guided project/tutorial on Udemy by Imran Teli. It serves as a practical exercise to reinforce the concepts learned during the tutorial.

## Project Objectives
The primary aim is to demonstrate the integration of various AWS services to establish a comprehensive CI/CD workflow. I started utilizing AWS CodeCommit for source code storage, replacing traditional repositories like GitHub. AWS CodeBuild generated artifact, offering flexibility with multiple build projects for diverse tasks such as code analysis and unit testing. Following this, artifacts found their home in S3 buckets before deployment using AWS CodeDeploy. My target deployment platform? AWS Beanstalk, where a Tomcat environment awaits. This environment is connected to an RDS database, ensuring seamless data management for my application. Finally, I orchestrated the entire process using AWS CodePipeline, automating deployments.

![app stack](https://github.com/debasishdtt/aws_cicd_project/assets/81139107/6ac112f3-c101-4a89-b5cb-a7d8f7b30a8d)

<p align="center">Fig. 1: Architectural design of the setup</p>

## Built with
* AWS CodeCommit: Source code storage solution within AWS.
* AWS CodeBuild: Service for building artifacts, supporting various tasks like code analysis and testing.
* Amazon S3: Object storage service for artifact storage.
* AWS CodeDeploy: Facilitates automated deployments to diverse targets, including AWS Beanstalk.
* AWS Beanstalk: Platform-as-a-Service offering for deploying and managing web applications.
* Amazon RDS: Relational Database Service for managing MySQL databases.
* AWS CodePipeline: Orchestrates the entire CI/CD process, automating deployments triggered by code changes.

## Deployment Process

1. Amazon Elastic Beanstalk
   
*Accessing Elastic Beanstalk: Navigate to the AWS Management Console and locate Elastic Beanstalk.
*Creating an Application: Click on "Create application" and provide a name for your application (e.g., vprofile).
*Creating an Environment: Select the desired environment type (e.g., Web Server Environment) and configure settings such as environment name, domain, platform (e.g., Tomcat), and application version.

*Configuration Details:
- Specify AWS Elastic Beanstalk service role.
- Choose a key pair for SSH access to EC2 instances (optional).
- Select VPC and subnet settings.
- Define auto-scaling parameters including minimum and maximum instances.
- Choose load balancer settings, listener configurations, and load balancer type.
* Additional Settings:
- Enable logging to S3 if necessary.
- Configure health reporting and rolling updates for deployment.
- Set up environment properties for backend services if required.
* Review and Launch: Carefully review all configurations before launching the environment.
* Deployment: Once launched, Beanstalk handles the provisioning, load balancing, auto-scaling, and health monitoring of underlying infrastructure.
* Verification: Verify the health status of the environment and access the default application URL provided by Beanstalk.
* Monitoring and Management: Monitor the environment status and resources from the Elastic Beanstalk dashboard. Make necessary adjustments or updates directly from Beanstalk.

2. Creating RDS Instance:
* Navigate to AWS Management Console and go to RDS.
* Click on "Create database" and select MySQL as the engine.
* Choose appropriate version and select free tier for instance type.
* Provide instance identifier, master username, and auto-generate password.
* Configure instance type (ensure it's T2.micro for free tier), storage, and connectivity.
* Add database name (e.g., 'accounts') under additional configuration.
* Review configurations, ensure free tier is selected, and create the database.
* Note down the endpoint and credentials for future use. 


