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
