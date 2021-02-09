# CI-CD
Implementing an end to end Continuous Integration and Continuous Delivery (CI/CD) Pipeline using AWS pipeline services like CodeCommit, CodeBuild, CodeDeploy and CodePipeline

Let us first understand what is a CI/CD Pipeline:

Stages in a Pipeline:
![Capture](https://github.com/roshnii20/CI-CD/blob/main/Pictures/Capture.PNG)

Continuous Integration (CI):

Continuous Integration is the step where all the developers work together on codes in a repository, make changes several times a day. With help of automated build, each commit is verified to detect problems/errors early on.

The difference between Continuous Delivery and Continuous Deployment (CD) :

Continuous Delivery(CD) is a process where the software release process is almost automated but still needs a manual approval before releasing it whereas Continuous Deployment eliminates all the manual steps including the approval so anyone with adequate priveleges can directly release the software. 


Here in this exercise, we will implement Continuous Integration and Continuous Delivery (CI/CD) pipeline on AWS.

We will need following two things to implement our Pipeline:
• AWS Account
• Virtual Machine ( Install Git on your local machine)

PART 1: CodeCommit
![CodeCommit](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CodeCommit.PNG)

CodeCommit is a secure, highly scalable, managed source control service that hosts private Git repositories. CodeCommit eliminates the need for you to manage your own source control system or worry about scaling its infrastructure. You can use CodeCommit to store anything from code to binaries. It supports the standard functionality of Git, so it works seamlessly with your existing Git-based tools.

STEP 1: One of the best practices while using AWS is making a new IAM user with relevant priveleges and login using that user and do the work, instead of using the root account. So here, we will create new IAM user and group with policies: “AdministratorAccess”,  “AWSCodeCommitFullAccess” and “AWSCodePipelineFullAccess”  and log back in using this user.

STEP 2: We will create an Amazon CloudWatch Events to detect and react to pipeline execution state changes by sending an Amazon SNS notification. You can create a new a subscription and choose any of the following as your endpoint: 

• HTTP/HTTPS
• Email/Email-JSON
• Amazon Kinesis Data Firehose
• AWS Lambda
• Amazon SQS
• Platform application endpoint
• SMS

STEP 3: Create a new repository on CodeCommit via console and connect it to your Virtual Machine using HTTPS


PART 2: CodeBuild
![CodeBuild](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CodeBuild.PNG)

AWS CodeBuild is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your own build servers. It provides prepackaged build environments for popular programming languages and build tools such as Apache Maven, Gradle, and more.

STEP 1: We will create an S3 bucket to store artifacts of CodeBuild


STEP 2: Create a buildspec.yml and appspec.yml on your Virtual Machine and push it to your CodeCommit repository from your Virtual Machine

A buildspec is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build.
An appspec is a YAML -formatted or JSON-formatted file used by CodeDeploy to manage a deployment.

*I have added both of these files in this repository* 

STEP 3: Create a new build 











