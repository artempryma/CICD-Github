## Walkthrough
The following steps provide a high-level overview of the walkthrough:

  1.	Clone the project from the AWS code samples repository.
  2.	Deploy the AWS CloudFormation template to create the required services.
  3.	Update the source code.
  4.	Setup GitHub secrets.
  5.	Integrate CodeDeploy with GitHub
  6.	Trigger the GitHub Action to build and deploy the code.
  7.	Verify the deployment.

## Deploying the CloudFormation template
To deploy the CloudFormation template, complete the following steps:

    1.	Open AWS CloudFormation console. Enter your account ID, user name and Password. 
    2.	Check your region, this solution uses us-east-1.
    3.	If this is  new AWS CloudFormation account, click Create New Stack. Otherwise, select Create Stack.
    4.	Select Template is Ready
    5.	Click Upload a template file
    6.	Click Choose File. Navigate to template.yml file in your cloned repository at “aws-codedeploy-github-actions-deployment/cloudformation/template.yaml” 
    7.	Select the template.yml file and select next.
    8.	In Specify Stack Details, add or modify values as needed.
            - Stack name = CodeDeployStack.
            - VPC and Subnets = (these are pre-populated for you) you can change these values if you prefer to use your own Subnets)
            - GitHubThumbprintList = 6938fd4d98bab03faadb97b34396831e3780aea1
            - GitHubRepoName – Name of your GitHub personal repository which you created.
    9.	On the Options page, click Next.
    10.	Select the acknowledgement box to allow the creation of IAM resources, and then select Create. 
    It will take CloudFormation about 5 minutes to create all the resources. This stack would create below resources.
           - Two EC2 Linux instances with Tomcat server and CodeDeploy agent installed 
           - Autoscaling group with Internet Application load balancer
           - CodeDeploy application name and deployment group
           - S3 bucket to store build artifacts
           - Identity and Access Management (IAM) OIDC identity provider
           - Instance profile for Amazon EC2 
           - Service role for CodeDeploy
           - Security groups for ALB and Amazon EC2


## Clean up

To avoid incurring future changes, you should clean up the resources that you created.

    1. Empty the Amazon S3 bucket:
    2. Delete the CloudFormation stack (CodeDeployStack) from the AWS console.
    3. Delete the GitHub Secret (‘IAMROLE_GITHUB’)
        1. Go to the repository settings on GitHub Page.
        2. Select Secrets under Actions.
        3. Select IAMROLE_GITHUB, and delete it.
