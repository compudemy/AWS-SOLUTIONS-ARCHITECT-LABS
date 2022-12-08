# AUTOMATED DEPLOYMENT OF EC2 WEB APPLICATION

# Introduction
This hands-on lab will guide you through the steps to configure a web application in Amazon EC2 with a defense in depth approach incorporating a number of AWS security best practices. The skills you learn will help you secure your workloads in alignment with the AWS Well-Architected Framework . The WordPress example CloudFormation template will deploy a basic WordPress content management system, This example is not intended to be a comprehensive WordPress system, please consult Build a WordPress Website for more information.

This lab will create the web application and all components using the example CloudFormation template, inside the VPC you have created previously. The components created include:

Application load balancer
Auto scaling group of web instances
A role attached to the auto-scaled instances allows temporary security credentials to be used
Instances use Systems Manager instead of SSH for administration
Amazon Aurora serverless database cluster
Secrets manager secret for database cluster
AWS Key Management Service is used for key management of Aurora database
Security groups for load balancer and web instances to restrict network traffic
Custom CloudWatch metrics and logs for web instances
IAM role for web instances that grants permission to Systems Manager and CloudWatch
Instances are configured from the latest Amazon Linux 2 Amazon Machine Image at boot time using user data to install agents and configure services
Overview of wordpress stack architecture:

![image](https://user-images.githubusercontent.com/103466963/205918713-a01d9b88-5923-4e4b-a7de-070a4e617a9b.png)

# NOTE: 
An SSH key is not configured in this lab, instead AWS Systems Manager should be used to manage the EC2 instances as a more secure and scalable method.
The Application Load Balancer will listen on unencrypted HTTP (port 80), it is a best practice to encrypt data in transit, you can configure a HTTPS listener after completion of this lab.
An example amazon-cloudwatch-agent.json file is provided and automatically downloaded by the instances to configure CloudWatch metrics and logs, this requires that you follow the example naming prefix of WebApp1.

# Prerequisites
An AWS account that you are able to use for testing.
Permissions to create resources in CloudFormation, EC2, VPC, IAM, Elastic Load Balancing, CloudWatch, Aurora RDS, KMS, Secrets Manager, Systems Manager.
Basic understanding of AWS CloudFormation , visit the Getting Started section of the user guide.
Deployed the CloudFormation VPC stack in the lab Automated Deployment of VPC .

# Costs
Typically less than $20 per month if the account is only used for personal testing or training, and the tear down is not performed:

EC2 instance default t3.micro X2 (default value) is $0.0208 per hour in us-east-1 region
Aurora serverless database default of 2 capacity units is $0.12 per hour in us-east-1 region
AWS KMS key for Aurora database is $1.00 per month plus $0.03 per 10,000 requests in us-east-1 region
Elastic Load Balancing, Application Load Balancer for Application Load Balancer is $0.0225 per hour in us-east-1 region
AWS Secrets Manager secret for database password is $0.40 per month
Amazon CloudWatch custom metrics X8 is $2.40 per month per instance in us-east-1 region
Amazon CloudWatch logs is $0.50 per GB in us-east-1 region
AWS Pricing

# Steps:
Create Web Stack

Tear down this lab

# CREATE WEB STACK

Please note a prerequisite to this lab is that you have deployed the CloudFormation 
VPC stack in the lab Automated Deployment of VPC with the default parameters and recommended stack name.

Choose the version of the CloudFormation template and download to your computer, or by cloning this repository:
wordpress.yaml to create a WordPress site, including an RDS database.
staticwebapp.yaml to create a static web application that simply displays the instance ID for the instance it is running upon.
Sign in to the AWS Management Console, select your preferred region, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/ . 
Note if your CloudFormation console does not look the same, you can enable the redesigned console by clicking New Console in the CloudFormation menu.

Click Create Stack, then With new resources (standard).

![image](https://user-images.githubusercontent.com/103466963/206483824-ad2b262f-066c-4c62-8058-4b8c4563a57a.png)

Click Upload a template file and then click Choose file.

![image](https://user-images.githubusercontent.com/103466963/206484642-1ffad6a8-2eed-4c93-bf3f-37298dacd553.png)

Choose the CloudFormation template you downloaded in step 1, return to the CloudFormation console page and click Next.
Enter the following details:

Stack name: The name of this stack. 
For this lab, for the WordPress stack use WebApp1-WordPress or for the static web stack use WebApp1-Static and match the case.

![image](https://user-images.githubusercontent.com/103466963/206485516-4c509729-e98d-42a8-8949-f6116084446d.png)

