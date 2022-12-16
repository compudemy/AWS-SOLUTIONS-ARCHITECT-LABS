# CLOUDFRONT FOR WEB APPLICATION

# Introduction
This hands-on lab will guide you through the steps to help protect a web application from network based attacks using Amazon CloudFront. You will use the AWS Management Console and AWS CloudFormation to guide you through how to deploy CloudFront. Skills learned will help you secure your workloads in alignment with the AWS Well-Architected Framework .

# Goals
Protecting network and host-level boundaries
System security configuration and maintenance
Enforcing service-level protection

# Prerequisites
An AWS account that you are able to use for testing, that is not used for production or other purposes. NOTE: You will be billed for any applicable AWS resources used if you complete this lab.
A web application to configure as the origin to CloudFront.

# Steps:

Configure CloudFront - EC2 or Load Balancer
Tear down


# CONFIGURE CLOUDFRONT - EC2 OR LOAD BALANCER

Using the AWS Management Console, we will create a CloudFront distribution, and link it to the AWS WAF ACL we previously created.

Open the Amazon CloudFront console at https://console.aws.amazon.com/cloudfront/home.
From the console dashboard, choose Create Distribution.

![image](https://user-images.githubusercontent.com/103466963/208147287-607ed034-861a-4384-9b2a-690e7827237f.png)

Click Get Started in the Web section.

![image](https://user-images.githubusercontent.com/103466963/208147331-88d1d22b-d0f4-4215-bdb6-694a4e0675ee.png)

Specify the following settings for the distribution:
In Origin Domain Name enter the DNS or domain name from your elastic load balancer or EC2 instance.

![image](https://user-images.githubusercontent.com/103466963/208147545-7afa1a4f-b35d-44d4-9833-813890e54dee.png)

Click Create Distribution.
For more information on the other configuration options, see Values That You Specify When You Create or Update a Web Distribution in the CloudFront documentation.
After CloudFront creates your distribution, the value of the Status column for your distribution will change from In Progress to Deployed.

![image](https://user-images.githubusercontent.com/103466963/208147659-bf9a0f97-a9b8-47d0-9ace-25884c17fdc2.png)

When your distribution is deployed, confirm that you can access your content using your new CloudFront URL or CNAME. Copy the Domain Name into a web browser to test.

![image](https://user-images.githubusercontent.com/103466963/208147888-623079fe-050d-4d60-bc23-de67a95532d6.png)

For more information, see Testing a Web Distribution in the CloudFront documentation. 7. You have now configured Amazon CloudFront with basic settings.



# TEAR DOWN

The following instructions will remove the resources that have a cost for running them. Please note that Security Groups and SSH key will exist. You may remove these also or leave for future use.

Delete the CloudFront distribution:

Open the Amazon CloudFront console at https://console.aws.amazon.com/cloudfront/home.
From the console dashboard, select the distribution you created earlier and click the Disable button. To confirm, click the Yes, Disable button.
After approximately 15 minutes when the status is Deployed, select the distribution and click the Delete button, and then to confirm click the Yes, Delete button.

