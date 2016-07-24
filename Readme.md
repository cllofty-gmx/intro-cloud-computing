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

## Gradle
The application is built using Gradle.  Download and install Gradle

https://gradle.org/getting-started-gradle-java/#toggle-id-1

## Configuring the application
You will need to configure the application with the AWS S3 storage credentials.  The application is configured via a application.properties file.  You will find a sample-application.properties file under "application/src/main/resources"

To configure the application -
* Make a copy of sample-application.properties.  Rename this copy to application.properties
* Enter the S3 bucket's name for the cloud.aws.s3.bucket property
* Enter your access key for the cloud.aws.credentials.accessKey property
* Enter you secret key for the cloud.aws.credentials.secretKey property
* If you selected a region other than US Standard when creating the S3 account, you will need to fill in the cloud.aws.region property.  The exact region string you need can be seen in the URL ("region=us-east-1")

Note, the application.properties file is ignored by Git to avoid accidentally checking in credentials to Github.

## Building
To build the application, run the build from the "application" folder.

    gradle build

The build command will create an executable JAR file that can be found in "application/build/libs".

## Running the Application
You can execute the JAR file using the following command

    java -jar ./build/libs/image-share-0.1.0.jar

The application should be running at http://localhost:8080/

There are some images in the "application/test-images" folder that you can use to verify your setup.
