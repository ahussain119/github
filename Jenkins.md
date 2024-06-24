# Jenkins Installation Guide

This guide will walk you through the steps to install Jenkins on an EC2 instance using the console.

## Prerequisites

Before you begin, make sure you have the following:

- An AWS account
- Access to the AWS Management Console

## Step 1: Launch an EC2 Instance

1. Log in to the AWS Management Console.
2. Navigate to the EC2 service.
3. Launch an Ubuntu EC2 instance using the `t3.medium` instance type.

## Step 2: Install Java 11

1. Connect to your EC2 instance using SSH.
2. Install Java 11 by running the following commands:

    ```bash
    sudo apt update
    sudo apt install openjdk-11-jdk wget xmllint
    ```

## Step 3: Install Jenkins

1. Add the Jenkins repository key to your system:

    ```bash
    wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
    ```

2. Add the Jenkins repository to your system:

    ```bash
    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    ```

3. Update your package list:

    ```bash
    sudo apt update
    ```

4. Install Jenkins:

    ```bash
    sudo apt install jenkins
    ```

## Step 4: Start Jenkins

1. Start the Jenkins service:

    ```bash
    sudo systemctl start jenkins
    ```

2. Enable Jenkins to start on boot:

    ```bash
    sudo systemctl enable jenkins
    ```

## Step 5: Access Jenkins

1. Open a web browser and navigate to `http://<your-ec2-instance-public-ip>:8080`, or preferably use the domain name.
2. Follow the on-screen instructions and install all the recommended plugins

You have successfully installed Jenkins on your EC2 instance.

## Step 6: Install Artifactory Nexus and Publish Over SSH Plugins
1. In the Jenkins dashboard, click on "Manage Jenkins" in the left sidebar.
2. Click on "Manage Plugins" to open the plugin manager.
3. Go to the "Available" tab and search for "Artifactory Nexus Plugin" and "Publish Over SSH Plugin".
4. Check the boxes next to both plugins and click on the "Install without restart" button.
5. Wait for the installation to complete.

## Step 7: Add Credentials for Nexus and Tomcat
1. In the Jenkins dashboard, click on "Manage Jenkins" in the left sidebar.
2. Click on "Credentials" to access the global credentials area.
3. Click on the desired domain or create a new one.
4. Click on "Add Credentials" to add a new credential.
5. For Nexus:
    - Select "Kind" as "Username with Password".
    - Enter the username and password for the Nexus repository.
6. For Tomcat:
    - Select "Kind" as "Username with Password".
    - Enter the username and password for the Tomcat server (e.g., username="deployer", password="deployer").
7. Save the credentials.

## Step 8: Install Maven
1. In the Jenkins dashboard, click on "Manage Jenkins" in the left sidebar.
2. Click on "Tools" to access the global tools configuration.
3. Scroll down to the "Maven" section and click on the "Add Maven" button.
4. Enter a name for the Maven installation and select the desired version from the dropdown menu.
5. Click on the "Save" button to install Maven automatically.
6. Jenkins will download and install the specified '3.5.6' version of Maven.
7. Once the installation is complete.

