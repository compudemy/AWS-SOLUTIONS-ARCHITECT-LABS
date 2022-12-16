# LEVEL 200

# CLOUDFRONT WITH WAF PROTECTION

# Introduction
This hands-on lab will guide you through the steps to protect a workload from network based attacks using Amazon CloudFront and AWS Web Application Firewall (WAF). 
You will use the AWS Management Console and AWS CloudFormation to guide you through how to deploy CloudFront with WAF integration to apply defense in depth methods. 
Skills learned will help you secure your workloads in alignment with the AWS Well-Architected Framework .

# Goals

Protecting network and host-level boundaries
System security configuration and maintenance
Enforcing service-level protection

# Prerequisites
An AWS account that you are able to use for testing, that is not used for production or other purposes. 
NOTE: You will be billed for any applicable AWS resources used if you complete this lab.

# Steps:

Launch Instance
Configure AWS WAF
Configure Amazon CloudFront
Tear down this lab


# LAUNCH INSTANCE

You can launch a Linux instance using the AWS Management Console. 
This tutorial is intended to help you launch your first instance quickly, so it doesn’t cover all possible options. 
For more information about the advanced options, see Launching an Instance . Launch an instance:

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

From the console dashboard, choose Launch Instance.

![image](https://user-images.githubusercontent.com/103466963/208150281-902e8ab9-47b2-4eab-a2ea-42aba1b250d3.png)

The choose an Amazon Machine Image (AMI) page displays a list of basic configurations, 
called Amazon Machine Images (AMIs), that serve as templates for your instance. Select the HVM edition of the Amazon Linux AMI, either version.

![image](https://user-images.githubusercontent.com/103466963/208150814-80358a51-71e3-416d-8a2f-b056ebfd9b15.png)

On the Choose an Instance Type page, you can select the hardware configuration of your instance. Select the t2.micro type, which is selected by default. Notice that this instance type is eligible for the free tier. Then select Next: Configure Instance Details.

![image](https://user-images.githubusercontent.com/103466963/208150951-d8b410ea-c86f-4451-ad2f-8a27ce60209a.png)

On the Configure Instance Details page, make the following changes:

5.1 Select Create new IAM role.

![image](https://user-images.githubusercontent.com/103466963/208151179-e65c695e-3761-4567-966c-b0f9241eed41.png)


5.2 In the new tab that opens, select Create role.


![image](https://user-images.githubusercontent.com/103466963/208151234-16a7a5a7-fba5-45aa-9b8b-595ec964bbd7.png)


5.3 With AWS service pre-selected, select EC2 from the top of the list, then click Next: Permissions.

![image](https://user-images.githubusercontent.com/103466963/208151431-af735b3a-762c-4d8d-b959-ec92e8b5f0ef.png)


5.4 Enter s3 in the search and select AmazonS3ReadOnlyAccess from the list of policies, then click Next: Review. This policy will give this EC2 instance access to read and list any objects in Amazon S3 within your AWS account.

![image](https://user-images.githubusercontent.com/103466963/208151474-3a2136a7-2481-40f8-97c4-8bee6052daaa.png)


5.5 Enter a role name, such as ec2-s3-read-only-role, and then click Create role.

![image](https://user-images.githubusercontent.com/103466963/208151531-a3c660b0-124d-42b7-8c95-67b38d8ac4e1.png)


5.6 Back on the EC2 launch web browser tab, select the refresh button next to Create new IAM role, and click the role you just created.

![image](https://user-images.githubusercontent.com/103466963/208151594-59dcc590-5c15-4b50-94bb-869a66eb3561.png)


5.7 Scroll down and expand the Advanced Details section. Enter the following in the User Data test box to automatically install Apache web server and apply basic configuration when the instance is launched:

#!/bin/bash
yum update -y
yum install -y httpd
service httpd start
chkconfig httpd on
groupadd www
usermod -a -G www ec2-user
chown -R root:www /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} +
find /var/www -type f -exec chmod 0664 {} +

Accept defaults and click Next: Add tags.

Click Next: Configure Security Group. 7.1 Accept default option Create a new security group. 7.2 On the line of the first default entry SSH, select Source as My IP. 7.3 Click Add Rule, select Type as HTTP and Source as Anywhere. Note that best practice is to have an Elastic Load Balancer inline or the EC2 instance not directly exposed to the internet. However, for simplicity in this lab, we are opening the access to anywhere. Other lab modules secure access with Elastic Load Balancer.

![image](https://user-images.githubusercontent.com/103466963/208151792-6451f6f8-e25a-4cf9-97ef-2caff6a82f14.png)


7.5 Click Review and Launch.

![image](https://user-images.githubusercontent.com/103466963/208151827-089c1e5b-3969-47f1-b492-6828fad56cc4.png)


On the Review Instance Launch page, check the details, and then click Launch.

If you do not have an existing key pair for access instances, a prompt will appear. Click Create New,then type a name such as lab, click Download Key Pair, and then click Launch Instances.

![image](https://user-images.githubusercontent.com/103466963/208151914-3685a6da-94af-425d-a217-0e510af340d3.png)


This is the only chance to save the private key file. You’ll need to provide the name of your key pair when you launch an instance, and you’ll provide the corresponding private key each time you connect to the instance.

Click View Instances.
When your instance is launched, its status will change to running, and it will need a few minutes to apply patches and install Apache web server.


![image](https://user-images.githubusercontent.com/103466963/208152007-dc4b7b69-99f7-4a0a-adba-57ead6ff685c.png)


You can connect to the Apache test page by entering the public DNS, which you can find on the description tab or instances list. Take note of this public DNS value.




# CONFIGURE AWS WAF
Using AWS CloudFormation , we are going to deploy a basic example AWS WAF configuration for use with CloudFront.

Sign in to the AWS Management Console, select your preferred region, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/. Note if your CloudFormation console does not look the same, you can enable the redesigned console by clicking New Console in the CloudFormation menu.

Click Create stack.

![image](https://user-images.githubusercontent.com/103466963/208152217-615abf62-89cc-4e82-8085-ba71603b4ea2.png)

Enter the following Amazon S3 URL: https://s3-us-west-2.amazonaws.com/aws-well-architected-labs/Security/Code/waf-global.yaml and click Next.

![image](https://user-images.githubusercontent.com/103466963/208152304-7992d65f-a641-4657-81ec-7020aaa586ad.png)

Enter the following details:
Stack name: The name of this stack. For this lab, use waf.
WAFName: Enter the base name to be used for resource and export names for this stack. For this lab, you can use Lab1.
WAFCloudWatchPrefix: Enter the name of the CloudWatch prefix to use for each rule using alphanumeric characters only. For this lab, you can use Lab1. The remainder of the parameters can be left as defaults.

![image](https://user-images.githubusercontent.com/103466963/208152353-b77483c9-9a89-44f3-976d-54feaa613503.png)

At the bottom of the page click Next.
In this lab, we won’t add any tags or other options. Click Next. Tags, which are key-value pairs, can help you identify your stacks. For more information, see Adding Tags to Your AWS CloudFormation Stack .
Review the information for the stack. When you’re satisfied with the configuration, click Create stack.
After a few minutes the stack status should change from CREATE_IN_PROGRESS to CREATE_COMPLETE.
You have now set up a basic AWS WAF configuration ready for CloudFront to use!




# CONFIGURE AMAZON CLOUDFRONT

Using the AWS Management Console, we will create a CloudFront distribution, and link it to the AWS WAF ACL we previously created.

Open the Amazon CloudFront console at https://console.aws.amazon.com/cloudfront/home.
From the console dashboard, choose Create Distribution.

![image](https://user-images.githubusercontent.com/103466963/208152528-4ca0b9c4-8f2b-4e1f-92a6-19177ba3e584.png)

Click Get Started in the Web section.

![image](https://user-images.githubusercontent.com/103466963/208152591-4fd30c32-01d4-4cbc-ab3f-9cc2f5a5e86c.png)


Specify the following settings for the distribution:
In Origin Domain Name enter the EC2 public DNS name you recorded from your instance launch.

![image](https://user-images.githubusercontent.com/103466963/208152647-22563a81-3ee5-4ded-810a-667ffcd71607.png)


In the distribution Settings section, click AWS WAF Web ACL, and select the one you created previously.

![image](https://user-images.githubusercontent.com/103466963/208152701-be912934-9c30-4dc3-ac17-76454d93625e.png)


Click Create Distrubution.
For more information on the other configuration options, see Values That You Specify When You Create or Update a Web Distribution in the CloudFront documentation.
After CloudFront creates your distribution, the value of the Status column for your distribution will change from In Progress to Deployed.

![image](https://user-images.githubusercontent.com/103466963/208152775-894abbf5-b7ca-481a-90d4-e1b97cc5edc3.png)


When your distribution is deployed, confirm that you can access your content using your new CloudFront URL or CNAME. Copy the Domain Name into a web browser to test.

![image](https://user-images.githubusercontent.com/103466963/208152820-7bf50364-f9b6-4093-856c-2819e67ba0e0.png)


For more information, see Testing a Web Distribution in the CloudFront documentation. 7. You have now configured Amazon CloudFront with basic settings and AWS WAF.

For more information on configuring CloudFront, see Viewing and Updating CloudFront Distributions in the CloudFront documentation.



# TEAR DOWN THIS LAB

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
