# Tomcat Installation Guide

This guide provides step-by-step instructions for installing Apache Tomcat on an EC2 instance using the AWS Management Console.

## Step 1: Launch an EC2 Instance

1. Log in to the AWS Management Console.
2. Go to the EC2 service.
3. Launch an Ubuntu EC2 instance with the `t2.medium` instance type.

## Step 2: Install Java 11

1. Connect to your EC2 instance using SSH.
2. Install Java 11 by running the following commands:

    ```bash
    sudo apt update
    sudo apt install openjdk-11-jdk wget xmllint
    ```

## Step 3: Install Tomcat

1. Download Apache Tomcat to your system:

    ```bash
    wget -q -O - https://downloads.apache.org/tomcat/tomcat-9/v9.0.50/bin/apache-tomcat-9.0.50.tar.gz | tar -xvzf -
    ```
    Update the version if needed.

2. Move the extracted Tomcat folder to the desired location:

    ```bash
    sudo mv apache-tomcat-* /opt/tomcat
    ```

3. Add the tomcat user and give permissions:

    ```bash
    sudo adduser tomcat
    sudo chown -R tomcat:tomcat /opt/tomcat
    ```

4. Give executing permissions to startup.sh and shutdown.sh which are under bin:

    ```bash
    sudo chmod +x /opt/tomcat/bin/startup.sh 
    sudo chmod +x /opt/tomcat/bin/shutdown.sh
    ```

5. Start Tomcat:

    ```bash
    /opt/tomcat/bin/startup.sh
    ```

6. Create a link for tomcat startup.sh and shutdown.sh:

    ```bash
    sudo ln -s /opt/tomcat/bin/startup.sh /usr/local/bin/tomcatup
    sudo ln -s /opt/tomcat/bin/shutdown.sh /usr/local/bin/tomcatdown
    ```

## Step 4: Access Tomcat

To allow remote login to the Tomcat Manager and Host Manager, you need to update the `context.xml` file. Follow these steps:

1. Navigate to the Tomcat installation directory.
2. Open the `webapps/host-manager/META-INF` folder.
3. Locate the `context.xml` file.
4. Open the `context.xml` file in a text editor.
5. Comment out the `Value ClassName` field on files which are under the webapp directory.
6. Save the changes and close the file.
7. Repeat steps 2-6 for the `webapps/manager/META-INF/context.xml` file.

Next, update the `tomcat-users.xml` file to add users with appropriate roles. Follow these steps:

1. Navigate to the Tomcat installation directory.
2. Open the `conf` folder.
3. Locate the `tomcat-users.xml` file.
4. Open the `tomcat-users.xml` file in a text editor.
5. Add the following lines inside the `<tomcat-users>` element:

```xml
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
<user username="deployer" password="deployer" roles="manager-script"/>
<user username="tomcat" password="s3cret" roles="manager-gui"/>
```

6. Save the changes and close the file.

Finally, restart the Tomcat service and try to log in to the Tomcat application from the browser. This time it should be successful.

1. Open a web browser and navigate to `http://<your-ec2-instance-public-ip>:8080`.
2. Optionally, you can edit the 'conf' file to have a different port to use on Tomcat, as Jenkins is using the same.
3. Follow the on-screen instructions to complete the Tomcat setup.

Congratulations! You have successfully installed Apache Tomcat on your EC2 instance.
