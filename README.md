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


STEP 2: Create a buildspec.yml and index.html on your Virtual Machine and push it to your CodeCommit repository from your Virtual Machine

A buildspec is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build.
Index.html is an index file that will show up a webpage when our pipeline is executed successfully

*I have added both these files in this repository* 

STEP 3: Create a new build 

Configure Project and Source as following:

![CB-1](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CB-1.png)

For Source, select AWS CodeCommit as Source provider and choose the CodeCommit repository you created earlier
![CB-2](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CB-2.png)

Artifacts specifies output settings for artifacts generated by an AWS CodeBuild build.

For configuring Artifacts, select the S3 bucket you created earlier and name the folder as Pipeline.zip ( you can choose any name but don't forget to add the .zip extension because of which all the artifacts would be consolidated into one zip file instead of many individual files.

![CB-3](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CB-3.png)

STEP 4: Start the build and select build type as single build

Successful build output:

![CB-5](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CB-5.png)

*If you run into any error while building, check the "phase details" to get detailed output*


PART 3: CodeDeploy
![CodeDeploy](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CodeDeploy.PNG)

CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

In this exercise, we will create an Elastic Beanstalk application which will be used later in CodeDeploy stage while adding stages in the pipeline in next part.

STEP 1: Create an Elastic Beanstalk application with PHP as your platform (Select defaults for platform branch & version) and use choose Upload source code origin as Public S3 URL and copy the URL of your zip file created earlier on S3 and add here

Successful output:

![CD-1](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CD-1.png)


PART 4: CodePipeline

![CP](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CodePipeline.PNG)

AWS CodePipeline is a continuous delivery service you can use to model, visualize, and automate the steps required to release your software. You can quickly model and configure the different stages of a software release process. CodePipeline automates the steps required to release your software changes continuously.

STEP: Create a pipeline by configuring CodeCommit as source stage, CodeBuild as build stage, Elastic Beanstalk as Deploy provider in deploy stage.

Successful output:

![CP-1](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CP-1.png)
![CP-2](https://github.com/roshnii20/CI-CD/blob/main/Pictures/CP-2.png)

You will also get notifications from SNS as soon as the the creation of pipeline is initiated

Click on the application URL and you will get your output as:

![OP-1](https://github.com/roshnii20/CI-CD/blob/main/Pictures/OP-1.png)


TRIGGERING PIPELINE:

Now to understand the working better, let us make some change to our index.html and push it to our repository.

Succesful output:

![OP-2](https://github.com/roshnii20/CI-CD/blob/main/Pictures/OP-2.png)

As soon as you push the changes made, it will trigger the pipeline and you will start recieving notifications from SNS again.

We have successfully implemented an end to end CI/CD Pipeline using AWS CodeCommit, CodeBuild, CodeDeploy and CodePipeline. 




















