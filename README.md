# Project Description

This project showcases the setup and deployment of a Java application using Jenkins, Maven, Tomcat, and Nexus. The project follows a pipeline approach, where the code is downloaded from a GitHub repository, built using Maven, and then sent to Nexus for artifact management. Another pipeline is responsible for downloading the artifact from Nexus and deploying it on Tomcat.

## Architecture Overview

The project consists of the following components:

1. Jenkins: Used as the CI/CD tool to automate the build and deployment process.
2. Maven: Used for building the Java application and managing dependencies.
3. Tomcat: The web server where the application will be deployed.
4. Nexus: The artifact repository used for storing and managing the built artifacts.

## First Pipeline Workflow

1. Code Download: The project code is downloaded from the GitHub repository.
2. Maven Build: The code is built using Maven, ensuring all dependencies are resolved.
3. Artifact Deployment: The built artifact is sent to Nexus for storage and version management.

## Second Pipeline Workflow
1. Artifact Downloaded: Latest artifact is downloaded from the Nexus artifactory tool
2. Tomcat Deployment: Retrieve is deployed to the Tomcat server.

## Getting Started

To get started with this project, follow these steps:

1. Clone the GitHub repository to your local machine.
2. Install Jenkins, Maven, Tomcat, and Nexus on separate EC2 instances.
3. Configure Jenkins to connect to the GitHub repository and set up the necessary pipelines.
4. Set up the Maven build configuration in Jenkins.
5. Configure Nexus as the artifact repository in Jenkins.
6. Set up the Tomcat server and configure it to deploy the artifacts from Nexus.

For detailed instructions, please refer to the project documentation.
