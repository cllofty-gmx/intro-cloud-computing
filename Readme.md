# Homework User Story

## User Story
As an instructor, I want an email that contains links to your services so that I can review your setup.

## Acceptance Criteria
* I should receive a single email per team
* The email should contain the name of the individuals on your team.
* The email should contain a link to your Github project
* Your Github project should contain a fork of this weeks repository
* The email should contain a public url to the image gallery application running on a AWS EC2 VM.
* I should be able to use the image gallery application to upload an image.

# Forking Repository
## Git
Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

Download and install Git -

https://git-scm.com/

If you are not familiar with Git, read the "Getting Started", "Git Basics" and "Git Branching" from the Git documentation -

https://git-scm.com/doc


## Github
You should create a free Github account if you do not have one already

https://github.com/

If you are new to Github, the sign up process has a link to help familiarize yourself with Github.

## The cmu-mis-iccfb repository
This class has a Github project where we will be sharing code.  For this assignment, fork the "intro-cloud-computing" repository.

https://github.com/cmu-mis-iccfb/intro-cloud-computing

You should use "git clone" to download the forked repository to your local computer.


# Setup Cloud Services

## Amazon Web Services
We will be using the free services in AWS for this class.  If you already have a standard Amazon account that you use, this account can be used to setup the AWS services.

https://aws.amazon.com/

### EC2
Launch an Ubuntu Server 14.04 LTS t2.micro EC2 instance that will host the image gallery application.

https://aws.amazon.com/ec2/

Enable HTTP in the Security Groups.

Don't loose the SSH keys!  You will not be able to manage your server without these keys.

#### SSH into EC2
You will use SSH to log into your EC2 instance.

On Windows, you can use Putty as an SSH client.

http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html

On Mac OSX and Linux, use the pre-existing SSH client -

http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html

#### Install Java 8 on your EC2 Instance
Your provisioned EC2 instance will need Java 8 to run the image gallery application.

SSH into your EC2 instance and run the following commands to install Java 8 -

    sudo add-apt-repository ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get install oracle-java8-installer

### S3
The image gallery application uses S3 to store the images.  You will need to setup a free S3 account.

https://aws.amazon.com/s3/

Create a bucket that will be used to store the images.

### Setting up Access
You will need to create an access key and a secret key for the services.  To create the key's select "Security Credentials" in the drop down menu associated with your name in the top right menu bar.

On the Security Credentials page, expand "Access Keys (Access Key ID and Secret Access Key)" and create a new access key.  You should download the credentials file.  The credentials file will be a CSV file that contains the access key and security key.

# Image Gallery Application
Throughout this course, we will be adding cloud services to a basic image gallery web application.  The base application is contained in the "application" folder in your forked repository.

## Java Development Kit (JDK) 8
The application's code uses some features found in JDK 8. Download the JDK

http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

## Configuring the application
You will need to configure the application with the AWS S3 storage credentials.  The application is configured via a application.properties file.  You will find a sample-application.properties file under "application/src/main/resources"

To configure the application -
* Make a copy of sample-application.properties.  Rename this copy to application.properties
* Enter the S3 bucket's name for the cloud.aws.s3.bucket property
* Enter your access key for the cloud.aws.credentials.accessKey property
* Enter you secret key for the cloud.aws.credentials.secretKey property
* If you selected a region other than US Standard when creating the S3 account, you will need to fill in the cloud.aws.region property.  The exact region string you need can be seen in the URL ("region=us-east-1") when logged into the AWS Developer Console

Note, the application.properties file is ignored by Git to avoid accidentally checking in credentials to Github.

## Building
The project uses Gradle as the build tool.  You can read more about Gradle here -

https://gradle.org/

The project provides a Gradle wrapper (gradlew).  The Gradle wrapper will download and install the appropriate Gradle version when a command is first executed.

To build the application, run the following Gradle command -

    gradlew build

The build command will create an executable JAR file that will be found in "application/build/libs".

## Running the Application Locally
You can execute the JAR file using the following command

    java -jar ./build/libs/image-share-0.1.0.jar

The application should be running at http://localhost:8080/

There are some images in the "application/test-images" folder that you can use to verify your setup.

## Running the Application on AWS EC2

You will need to transfer the applications JAR file to your running EC2 instance.  The Secure Copy Client (SCP) is the best way to transfer files.

On Windows, you can either use Putty SCP or WinSCP.  Follow the file transfer instructions on this page -

http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html

On OSX or Linux, use the pre-existing SCP client.  Follow the file transfer instructions on this page -

http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html

To run the application -
1.  Log into your EC2 instance using SSH
2.  Make an "image-gallery" directory with the following command - ``mkdir image-gallery``
3.  Use SCP to transfer the application JAR file to the new directory
4.  Follow the information below to launch the application

To launch the application, run the following command -
    sudo nohup java -Dserver.port=80 -jar image-share-0.1.0.jar &

Breaking this command down -
* ``nohup`` will keep the process running after you close the SSH session
* ``-Dserver.port=80`` tells the application server to listen on the default HTTP port 80 for incoming connections
* ``&`` at the end of the command runs the command in the background.
* The logging output is redirected to ``nohup.out``.  This file will contain information for debugging.

Once the application is running in the background, you will need to kill the process when updating the application.  You will need the Process ID (PID) to kill the process.

To find the PID, run the following command -

    sudo ps ax | grep nohup

The first number printed in the output is the PID.  You can use the ``kill`` command to stop the process -

    sudo kill <<PID>>
