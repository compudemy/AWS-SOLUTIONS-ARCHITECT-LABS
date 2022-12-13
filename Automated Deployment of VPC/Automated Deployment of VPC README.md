# AUTOMATED DEPLOYMENT OF VPC

# Introduction
This hands-on lab will use AWS CloudFormation to create an Amazon VPC to outline some of the AWS security features available. Using CloudFormation to automate the deployment provides a repeatable way to create and update, and you can re-use the template after this lab.

The example template will deploy a completely new VPC incorporating a number of AWS security best practices which include:

Networking subnets created in 3 availability zones for the following network tiers:

Application Load Balancer - named ALB1
Application instances - named App1
Shared services - named Shared1
Database - named DB1

# VPC Architecture:

![image](https://user-images.githubusercontent.com/103466963/207374229-54a70859-1199-4344-83ca-b28777bd8da2.png)

VPC endpoints are created for private connectivity to AWS services. Additional endpoints can be enabled for the application tier using the App1SubnetsPrivateLinkEndpoints CloudFormation parameter.
NAT Gateways are created to allow subnets in the VPC to connect to the internet, without any direct ingress access as defined by the Route Table .
Network ACLs control access at each subnet tier.
VPC Flow Logs captures information about IP traffic and stores it in Amazon CloudWatch Logs.

# Requirements
An AWS account that you are able to use for testing, that is not used for production or other purposes.
An IAM user or role in your AWS account with access to CloudFormation, EC2, VPC, IAM.
Basic understanding of AWS CloudFormation , visit the Getting Started section of the user guide.

# NOTE: 
You will be billed for any applicable AWS resources used if you complete this lab that are not covered in the AWS Free Tier. 
It is recommended to delete the CloudFormation stack when you have completed the lab.

# Steps:
Create VPC Stack
Tear Down



# CREATE VPC STACK

This step will create the VPC and all components using the example CloudFormation template.

Download the latest version of the CloudFormation template here: vpc-alb-app-db.yaml

Go to the AWS CloudFormation console at https://console.aws.amazon.com/cloudformation and click Create Stack > With new resources

![image](https://user-images.githubusercontent.com/103466963/207377082-354103d2-8345-4ad7-81cc-563db4098384.png)

Leave Prepare template setting as-is

For Template source select Upload a template file
Click Choose file and supply the CloudFormation template you downloaded: vpc-alb-app-db.yaml

![image](https://user-images.githubusercontent.com/103466963/207377197-be593ecc-3cad-46ee-8497-356e6dd372e2.png)

Click Next

For Stack name use WebApp1-VPC

Parameters

Look over the Parameters and their default values.

Leave all parameters as their default values unless you are experimenting.

Click Next

For Configure stack options we recommend configuring tags, which are key-value pairs, that can help you identify your stacks and the resources they create. For example, enter Owner in the left column which is the key, and your email address in the right column which is the value. We will not use additional permissions or advanced options so click Next. For more information, see Setting AWS CloudFormation Stack Options .

For Review

Review the contents of the page
At the bottom of the page, select I acknowledge that AWS CloudFormation might create IAM resources with custom names

Click Create stack

![image](https://user-images.githubusercontent.com/103466963/207377429-b67eb396-dc62-4ae8-b758-d767f02f07de.png)

This will take you to the CloudFormation stack status page, showing the stack creation in progress.

Click on the Events tab
Scroll through the listing. It shows the activities performed by CloudFormation (newest events at top), such as starting to create a resource and then completing the resource creation.
Any errors encountered during the creation of the stack will be listed in this tab.

![image](https://user-images.githubusercontent.com/103466963/207377523-6168db2a-1bc7-4f9b-a4fc-0f2392223985.png)


When it shows status CREATE_COMPLETE, then you are finished with this step.

Now that you have a new VPC, check out 200_Automated_Deployment_of_EC2_Web_Application to deploy an example web application inside it.



# TEAR DOWN

The following instructions will remove the resources that you have created in this lab.

Note: If you are planning on completing the lab 200_Automated_Deployment_of_EC2_Web_Application we recommend you only tear down this lab after completing both, as there is a dependency on this VPC.

Delete the VPC CloudFormation stack:

Sign in to the AWS Management Console, select your preferred region, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/ .
Click the radio button on the left of the WebApp1-VPC stack.
Click the Actions button then click Delete stack.
Confirm the stack and then click Delete button.
Delete the CloudWatch Logs:

Sign in to the AWS Management Console, select your preferred region, and open the CloudFormation console at https://console.aws.amazon.com/cloudwatch/ .
Click Logs in the left navigation.
Click the radio button on the left of the WebApp1-VPC-VPCFlowLogGroup-<some unique ID>.
Click the Actions Button then click Delete Log Group.
Verify the log group name then click Yes, Delete.

