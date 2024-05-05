<h1 align="center" id="title">AWS CI/CD Project</h1>

# Introduction
<p>The project is about focusing on integrating AWS services to construct a robust CI/CD pipeline entirely within the AWS environment.</p>

<h5>🌟About</h5>
This project was developed as part of a guided project/tutorial on Udemy by Imran Teli. It serves as a practical exercise to reinforce the concepts learned during the tutorial.

# Project Objectives
The primary aim is to demonstrate the integration of various AWS services to establish a comprehensive CI/CD workflow. I started utilizing AWS CodeCommit for source code storage, replacing traditional repositories like GitHub. AWS CodeBuild generated artifact, offering flexibility with multiple build projects for diverse tasks such as code analysis and unit testing. Following this, artifacts found their home in S3 buckets before deployment using AWS CodeDeploy. My target deployment platform? AWS Beanstalk, where a Tomcat environment awaits. This environment is connected to an RDS database, ensuring seamless data management for my application. Finally, I orchestrated the entire process using AWS CodePipeline, automating deployments.

![app stack](https://github.com/debasishdtt/aws_cicd_project/assets/81139107/6ac112f3-c101-4a89-b5cb-a7d8f7b30a8d)

<p align="center">Fig. 1: Architectural design of the setup</p>

# Built with
* AWS CodeCommit: Source code storage solution within AWS.
* AWS CodeBuild: Service for building artifacts, supporting various tasks like code analysis and testing.
* Amazon S3: Object storage service for artifact storage.
* AWS CodeDeploy: Facilitates automated deployments to diverse targets, including AWS Beanstalk.
* AWS Beanstalk: Platform-as-a-Service offering for deploying and managing web applications.
* Amazon RDS: Relational Database Service for managing MySQL databases.
* AWS CodePipeline: Orchestrates the entire CI/CD process, automating deployments triggered by code changes.

# Deployment Process

## Amazon Elastic Beanstalk
   
* Accessing Elastic Beanstalk: Navigate to the AWS Management Console and locate Elastic Beanstalk.
* Creating an Application: Click on "Create application" and provide a name for your application (e.g., vprofile).
* Creating an Environment: Select the desired environment type (e.g., Web Server Environment) and configure settings such as environment name, domain, platform (e.g., Tomcat), and application version.

1. Configuration Details:
* Specify AWS Elastic Beanstalk service role.
* Choose a key pair for SSH access to EC2 instances (optional).
* Select VPC and subnet settings.
* Define auto-scaling parameters including minimum and maximum instances.
* Choose load balancer settings, listener configurations, and load balancer type.
2. Additional Settings:
* Enable logging to S3 if necessary.
* Configure health reporting and rolling updates for deployment.
* Set up environment properties for backend services if required.
* Review and Launch: Carefully review all configurations before launching the environment.
* Deployment: Once launched, Beanstalk handles the provisioning, load balancing, auto-scaling, and health monitoring of underlying infrastructure.
* Verification: Verify the health status of the environment and access the default application URL provided by Beanstalk.
* Monitoring and Management: Monitor the environment status and resources from the Elastic Beanstalk dashboard. Make necessary adjustments or updates directly from Beanstalk.

3. Creating RDS Instance:
* Navigate to AWS Management Console and go to RDS.
* Click on "Create database" and select MySQL as the engine.
* Choose appropriate version and select free tier for instance type.
* Provide instance identifier, master username, and auto-generate password.
* Configure instance type (ensure it's T2.micro for free tier), storage, and connectivity.
* Add database name (e.g., 'accounts') under additional configuration.
* Review configurations, ensure free tier is selected, and create the database.
* Note down the endpoint and credentials for future use. 

## AWS CodeCommit
These steps provide a guide to setting up AWS CodeCommit, configuring IAM user access, SSH authentication, and transitioning from GitHub to CodeCommit.

1. Create AWS CodeCommit Repository:
* Navigate to the AWS Management Console and select the CodeCommit service.
* Click on "Create repository" and provide a name for your repository (e.g., "V Profile").
* Optionally, you can add a description and tags.
* You can enable Amazon CodeGuru for Java projects for code quality analysis.
* Create the repository and note the HTTPS and SSH clone URLs.
2. Set Up IAM User:
* Go to the IAM service from the AWS Management Console.
* Create a new IAM user with programmatic access.
* Assign a relevant policy to the user. In this case, a policy specifically granting access to the CodeCommit repository is created.
* After creating the policy, assign it to the IAM user.
* Once the user is created, ensure that access keys are not needed and delete them if present.
* Upload the SSH public key for authentication.
3. Configure SSH:
* Generate SSH keys on your local machine using ssh-keygen.
* Upload the generated SSH public key to AWS CodeCommit.
* Create an SSH config file with the appropriate settings for CodeCommit.
* Set the permissions of the config file to 600.
4. Test SSH Authentication:
* Test SSH authentication by running a command like ssh <URL>.
5. Clone Repository (Optional, for testing):
* Clone the repository using the SSH URL to ensure that the IAM user has the required privileges.
6. Transition from GitHub to CodeCommit:
* If transitioning from GitHub, ensure you have the source code locally.
* Check out each branch locally using a loop to automate the process if necessary.
* Fetch tags if they exist.
* Remove the existing GitHub origin and add the CodeCommit repository as the new origin.
* Push all branches and tags to the CodeCommit repository.
7. Navigate to CodeBuild Service:
* Access the CodeBuild service from the AWS Management Console.
8. Create a CodeBuild Project:
* Click on "Create project".
* Specify the project name (e.g., "vprofile build").
* Configure the source code location, which can be from GitHub, Bitbucket, GitHub Enterprise, Amazon S3, or CodeCommit. Select the CodeCommit repository and the desired branch.
* Choose the operating system for the build environment. In this case, select Ubuntu.
* Specify the environment type (Linux, Windows).
* Review and configure the compute size based on your requirements.
* Define the build commands or use a build specification file (buildspec.yaml).
* Switch to the editor to write the build specification file.
9. Write Build Specification (buildspec.yaml):
* Use version 0.2 of the build specification.
* Define phases such as install, pre build, build, and post build.
* In the install phase, specify the runtime version and packages to install.
* In the pre build phase, run commands such as updating packages and installing necessary tools.
* Use sed commands in the pre build phase to search and replace values in application properties files with RDS values.
* Specify build commands such as MVN install in the build phase.
* Define the artifacts to upload to Amazon S3 after the build completes.
10. Upload Artifacts to Amazon S3:
* Specify the S3 bucket where artifacts will be uploaded.
* Configure artifact packaging options if needed.
11. Configure Logs:
* Choose whether to stream logs to Amazon CloudWatch Logs.
* Provide a log group name.
12. Create the Build Project:
* Review the project configuration.
* Ensure that there are no conflicting role or policy names.
* Click on "Create build project" to create the project.
13. Troubleshoot Any Errors:
* If there are any errors during project creation, such as existing role or policy names, resolve them by deleting conflicting roles or policies.

## Build, Deploy & Code Pipeline

1. Testing the Build Job:
* Access the CodeBuild service from the AWS Management Console.
* Create a CodeBuild project with the necessary configurations, including source code location, build environment, and build commands specified in a build specification file (buildspec.yaml).
* Write the build specification file, defining the phases such as install, pre build, build, and post build.
* Upload artifacts to an Amazon S3 bucket.
* Configure logs to stream to Amazon CloudWatch Logs.
* Start the build job and monitor its progress through the phase details.
* Verify that each phase completes successfully and that the artifact is uploaded to the specified S3 bucket.

<img width="973" alt="source_build_deploy_succeded" src="https://github.com/debasishdtt/aws_cicd_project/assets/81139107/7a5065fe-add2-4c0e-afd8-489d7019791d">

<p align="center">Fig. 2: Source Build Deploy Succeded.</p>

2. Integrating into a CI/CD Pipeline:
* Access the AWS CodePipeline service from the AWS Management Console.
* Create a new pipeline and give it a name (e.g., "vprofile CICD Pipeline").
* Configure advanced settings such as encryption and CloudWatch Events for source code detection.
* Select the source code provider (e.g., CodeCommit) and specify the repository and branch to monitor for changes.
* Choose the build provider (e.g., CodeBuild) and select the previously created CodeBuild project.
* Optionally, add additional actions to the pipeline such as unit testing or manual approval.
* Save and create the pipeline.
* Monitor the pipeline as it automatically triggers builds upon detecting changes in the source code repository.
* Verify that the deployment stage successfully deploys the artifact to the Beanstalk environment.

<img width="960" alt="webpage" src="https://github.com/debasishdtt/aws_cicd_project/assets/81139107/2e77e495-b6bd-4e55-8907-ad30d3caae5e">

<p align="center">Fig. 3: Successful access to the desired site.</p>

# Conclusion

In conclusion, the "AWS CI/CD Project" serves as a comprehensive demonstration of integrating various AWS services to construct a robust CI/CD pipeline entirely within the AWS environment. Under the guidance of Imran Teli's tutorial on Udemy, the project aims to reinforce the concepts of CI/CD workflows by leveraging AWS CodeCommit, CodeBuild, S3, CodeDeploy, Beanstalk, RDS, and CodePipeline.

The project's architectural design, as depicted in Figure 1, illustrates the seamless integration of AWS services, starting from source code storage in CodeCommit to automated deployments using CodePipeline. The deployment process involves setting up Amazon Elastic Beanstalk environments, configuring RDS instances, and orchestrating the entire process through AWS CodePipeline.

Key highlights include the utilization of AWS services for different stages of the deployment process, such as:

CodeCommit for source code management,
CodeBuild for artifact generation and build tasks,
Amazon S3 for artifact storage,
CodeDeploy for automated deployments to AWS Beanstalk environments, and
CodePipeline for orchestrating the entire CI/CD workflow.
The project's deployment process is meticulously outlined, providing step-by-step instructions for setting up Elastic Beanstalk environments, creating RDS instances, configuring CodeCommit repositories, and creating CodeBuild projects. Furthermore, the integration into a CI/CD pipeline through AWS CodePipeline streamlines the deployment process, automating builds triggered by code changes.

Figure 2 and Figure 3 showcase successful build and deployment outcomes, demonstrating the effectiveness of the CI/CD pipeline implemented in the project. Overall, the project serves as a practical exercise to deepen understanding and proficiency in leveraging AWS services for seamless and efficient software deployment workflows within the AWS ecosystem.

# Room for Growth

While AWS CodeDeploy is used for automated deployments to AWS Beanstalk environments, exploring advanced deployment strategies like blue-green deployments or canary releases can minimize downtime and risk during deployment, ensuring a seamless experience for end-users. Incorporating robust monitoring and observability practices, such as leveraging AWS CloudWatch metrics, alarms, and logs, as well as implementing distributed tracing and logging solutions, can provide valuable insights into application performance, identify bottlenecks, and facilitate timely troubleshooting and optimization.
