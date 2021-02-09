# CI-CD
Implementing an end to end Continuous Integration and Continuous Delivery (CI/CD) Pipeline using AWS pipeline services like CodeCommit, CodeBuild, CodeDeploy and CodePipeline

Let us first understand what is a CI/CD Pipeline:

Stages in a Pipeline:
![Capture](https://github.com/roshnii20/CI-CD/blob/main/Capture.PNG)

Continuous Integration (CI):

Continuous Integration is the step where all the developers work together on codes in a repository, make changes several times a day. With help of automated build, each commit is verified to detect problems/errors early on.

The difference between Continuous Delivery and Continuous Deployment (CD) :

Continuous Delivery(CD) is a process where the software release process is almost automated but still needs a manual approval before releasing it whereas Continuous Deployment eliminates all the manual steps including the approval so anyone with adequate priveleges can directly release the software. 


Here in this exercise, we will implement Continuous Integration and Continuous Delivery (CI/CD) pipeline on AWS.

We will need following two things to implement our Pipeline:
• AWS Account

• Virtual Machine

PART 1: CodeCommit
![CodeCommit](https://github.com/roshnii20/CI-CD/blob/main/CodeCommit.PNG)

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








