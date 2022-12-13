# AUTOMATED DEPLOYMENT OF WEB APPLICATION

# Introduction
This hands-on lab will guide you through the steps to protect a workload from network based attacks using AWS Web Application Firewall (WAF) integrated with Amazon CloudFront. 
You will use the AWS Management Console and AWS CloudFormation to guide you through how to deploy AWS Web Application Firewall (WAF) with CloudFront integration to apply defense in depth methods. 
Skills learned will help you secure your workloads in alignment with the AWS Well-Architected Framework .

# Goals

Protecting network and host-level boundaries
System security configuration and maintenance
Enforcing service-level protection

# Prerequisites

An AWS account that you are able to use for testing, that is not used for production or other purposes. 
NOTE: You will be billed for any applicable AWS resources used if you complete this lab.

# Steps:
Configure AWS WAF
Configure Amazon CloudFront
Tear down




# CONFIGURE AWS WAF

Using AWS CloudFormation , we are going to deploy a basic example AWS WAF configuration for use with CloudFront.

Sign in to the AWS Management Console, select your preferred region, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/. Note if your CloudFormation console does not look the same, you can enable the redesigned console by clicking New Console in the CloudFormation menu.
Click Create stack.

![image](https://user-images.githubusercontent.com/103466963/207380385-ba587c74-b3b7-4940-9f07-5d05207a0817.png)

Enter the following Amazon S3 URL: https://s3-us-west-2.amazonaws.com/aws-well-architected-labs/Security/Code/waf-global.yaml and click Next.

![image](https://user-images.githubusercontent.com/103466963/207380461-2869cc49-746d-417a-801b-6652e84735b9.png)

Enter the following details:
Stack name: The name of this stack. For this lab, use waf.
WAFName: Enter the base name to be used for resource and export names for this stack. For this lab, you can use Lab1.
WAFCloudWatchPrefix: Enter the name of the CloudWatch prefix to use for each rule using alphanumeric characters only. For this lab, you can use Lab1. The remainder of the parameters can be left as defaults.

![image](https://user-images.githubusercontent.com/103466963/207380572-49ef526e-f323-4d64-8003-dadc0410a920.png)

At the bottom of the page click Next.
In this lab, we won’t add any tags or other options. Click Next. Tags, which are key-value pairs, can help you identify your stacks. For more information, see Adding Tags to Your AWS CloudFormation Stack .
Review the information for the stack. When you’re satisfied with the configuration, click Create stack.
After a few minutes the stack status should change from CREATE_IN_PROGRESS to CREATE_COMPLETE.
You have now set up a basic AWS WAF configuration ready for CloudFront to use!

CONFIGURE AMAZON CLOUDFRONT
Using the AWS Management Console, we will create a CloudFront distribution, and link it to the AWS WAF ACL we previously created.

Open the Amazon CloudFront console at https://console.aws.amazon.com/cloudfront/home.
From the console dashboard, choose Create Distribution.

![image](https://user-images.githubusercontent.com/103466963/207380795-cb4dc934-f24c-44de-9306-8cf2422fa2e6.png)


Click Get Started in the Web section.

![image](https://user-images.githubusercontent.com/103466963/207380843-730a9db7-daea-4a49-8e25-ee9177ea8f58.png)


Specify the following settings for the distribution:
In Origin Domain Name enter the DNS or domain name from your elastic load balancer or EC2 instance.

![image](https://user-images.githubusercontent.com/103466963/207380936-0b579253-a135-4ac7-a198-9139efd95c3f.png)


In the distribution Settings section, click AWS WAF Web ACL, and select the one you created previously.

![image](https://user-images.githubusercontent.com/103466963/207381009-d8811e6c-8f9a-4a8a-a306-b754b6315234.png)


Click Create Distrubution.
For more information on the other configuration options, see Values That You Specify When You Create or Update a Web Distribution in the CloudFront documentation.
After CloudFront creates your distribution, the value of the Status column for your distribution will change from In Progress to Deployed.

![image](https://user-images.githubusercontent.com/103466963/207381107-950bf035-e1d4-4ba3-9bd5-3bf8dd1095e2.png)


When your distribution is deployed, confirm that you can access your content using your new CloudFront URL or CNAME. Copy the Domain Name into a web browser to test.

![image](https://user-images.githubusercontent.com/103466963/207381182-aa18ea88-34cf-477e-b77d-1bbe6ae07711.png)


For more information, see Testing a Web Distribution in the CloudFront documentation.

You have now configured Amazon CloudFront with basic settings and AWS WAF.
For more information on configuring CloudFront, see Viewing and Updating CloudFront Distributions in the CloudFront documentation.



# TEAR DOWN
The following instructions will remove the resources that have a cost for running them. Please note that Security Groups and SSH key will exist. You may remove these also or leave for future use.

Delete the CloudFront distribution:

Open the Amazon CloudFront console at https://console.aws.amazon.com/cloudfront/home.
From the console dashboard, select the distribution you created earlier and click the Disable button. To confirm, click the Yes, Disable button.
After approximately 15 minutes when the status is Deployed, select the distribution and click the Delete button, and then to confirm click the Yes, Delete button.
Delete the AWS WAF stack:

Sign in to the AWS Management Console, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/.
Select the waf-cloudfront stack.
Click the Actions button, and then click Delete Stack.
Confirm the stack, and then click the Yes, Delete button.
