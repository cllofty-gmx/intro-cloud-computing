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

# Setup Cloud Services
## Git
Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

Download and install Git -

https://git-scm.com/

If you are not familiar with Git, read the "Getting Started", "Git Basics" and "Git Branching" from the Git documentation -

https://git-scm.com/doc


## Github
You should create a free Github account if you do not have one already

https://github.com/

If you are new to Github, the sign process has a link to help familiarize yourself with Github.

## The cmu-mis-iccfb project
This class has a Github project where we will be sharing code.  For this assignment, fork the "intro-cloud-computing" repository.

https://github.com/cmu-mis-iccfb/intro-cloud-computing

## Amazon Web Services
We will be using the free services in AWS for this class.  If you already have a standard Amazon account that you use, this account can be used to setup the AWS services.

https://aws.amazon.com/

### EC2
Launch an Ubuntu Server 14.04 LTS t2.micro EC2 instance that will host the image gallery application.

https://aws.amazon.com/ec2/

Enable HTTP in the Security Groups.

Don't loose the SSH keys!  You will not be able to manage your server with out these keys.

### S3
The image gallery application uses S3 to store the images.  You will need to setup a free S3 account.

https://aws.amazon.com/s3/
