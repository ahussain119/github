# Nexus Installation Guide

This guide provides step-by-step instructions for installing Nexus on an EC2 instance using the AWS Management Console.

## Step 1: Launch an EC2 Instance

1. Log in to the AWS Management Console.
2. Go to the EC2 service.
3. Launch an Ubuntu EC2 instance with the `t3.XLarge` instance type.

## Step 2: Install Java 11

1. Connect to your EC2 instance using SSH.
2. Install Java 11 by running the following commands:

    ```bash
    sudo apt update
    sudo apt install wget
    sudo apt install openjdk-11-jdk
    ```

## Step 3: Install Nexus

1. Downlaod  Nexus to your system:

    ```bash
    wget -q -O - https://download.sonatype.com/nexus/3/latest-unix.tar.gz | tar -xvz
    ```

2. Move the extracted Nexus folder to the desired location:

    ```bash
    sudo mv nexus-3.x.x-xx /opt/nexus
    sudo mv sonatype-work /opt/nexus
    ```

3. Add nexus user and give permissions

    ```bash
    sudo adduser nexus
    sudo chown -R nexus:nexus /app/nexus
    sudo chown -R nexus:nexus /sonatype-work
    ```

4. Edit user in nexus.rc

    ```bash
    sudo vi /opt/nexus/bin/nexus.rc
    ```
    Edit the text us following and remove #

    ```bash
    run_as_user="nexus"
    ```
5. start nexus
    ```bash
    ./nexus/bin/nexus start
    ```

## Step 4: Access Nexus

1. Open a web browser and navigate to `http://<your-ec2-instance-public-ip>:8081`.
2. Follow the on-screen instructions to complete the Nexus setup.

Congratulations! You have successfully installed Nexus on your EC2 instance.

## Step 5: Creating the Repository and Updating the Configuration
1. Login to Nexus.
2. Go to "Settings" and select "Repository".
3. Click on "Create New" and choose "Maven2 (Host)".
4. Select the version as "Mixed".
5. Set the content description as "Inline".
6. Choose the deployment policy as "Allow Redeploy".
7. Save the configuration.
