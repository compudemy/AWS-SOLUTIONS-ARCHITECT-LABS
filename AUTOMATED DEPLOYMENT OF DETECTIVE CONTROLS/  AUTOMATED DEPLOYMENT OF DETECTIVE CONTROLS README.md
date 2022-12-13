# Introduction

This hands-on lab will guide you through how to use AWS CloudFormation to automatically configure detective controls including AWS CloudTrail, AWS Config, Amazon GuardDuty, and AWS Security Hub. 
You will use the AWS Management Console and AWS CloudFormation to automate the configuration of each service. 
The skills you learn will help you secure your workloads in alignment with the AWS Well-Architected Framework .

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. 
With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. 
CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services.

AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources. 
AWS Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations.

Amazon GuardDuty is a threat detection service that continuously monitors for malicious or unauthorized behavior to help you protect your AWS accounts and workloads. It monitors for activity such as unusual API calls or potentially unauthorized deployments that indicate a possible account compromise. GuardDuty also detects potentially compromised instances or reconnaissance by attackers.

AWS Security Hub is a service that aggregates, organizes, and prioritizes your security alerts, or findings, from multiple AWS services, such as Amazon GuardDuty, Amazon Inspector, Amazon Macie, AWS Identity and Access Management (IAM) Access Analyzer, AWS Systems Manager, and AWS Firewall Manager, as well as from AWS Partner Network (APN) solutions. AWS Security Hub continuously monitors your environment using automated security checks based on the AWS best practices and industry standards that your organization follows.

# Prerequisites

An AWS account that you are able to use for testing.
Permissions to create resources in CloudFormation, CloudTrail, GuardDuty, Config, S3, CloudWatch.

# Costs

Typically less than $2 per month if the account is only used for personal testing or training, and the tear down is not performed
AWS CloudTrail pricing
Amazon GuardDuty pricing
AWS Config pricing
Amazon S3 pricing
AWS Security Hub pricing
AWS Pricing

# Steps:

Create Stack
Knowledge Check
Tear down

# CREATE STACK

Creating this CloudFormation stack will configure CloudTrail including a new trail, an S3 bucket, and a CloudWatch Logs group for CloudTrail logs. You can optionally configure AWS Config and Amazon GuardDuty by setting the CloudFormation parameter for each.

Download the latest version of the CloudFormation template here: cloudtrail-config-guardduty-securityhub.yaml

Go to the AWS CloudFormation console at https://console.aws.amazon.com/cloudformation and click Create Stack > With new resources

![image](https://user-images.githubusercontent.com/103466963/205398006-82029680-0310-4e1c-8f97-e8a59b180772.png)

Leave Prepare template setting as-is

For Template source select Upload a template file
Click Choose file and supply the CloudFormation template you downloaded: cloudtrail-config-guardduty-securityhub.yaml

![image](https://user-images.githubusercontent.com/103466963/205398042-624893fe-dbf2-4b25-b867-0a356d388f00.png)

Click Next

For Stack name use DetectiveControls

Parameters

Look over the Parameters and their default values.

Under General section only enable the service if you have not configured already. CloudTrail is enabled by default, if you have enabled already this will create another trail and S3 bucket.

CloudTrailBucketName: The name of the new S3 bucket to create for CloudTrail to send logs to.

IMPORTANT: Bucket names need to be unique across all AWS buckets, and only contain lowercase letters, numbers, and hyphens.

ConfigBucketName: The name of the new S3 bucket to create for Config to save config snapshots to.

GuardDutyEmailAddress: The email address you own that will receive the alerts, you must have access to this address for testing.

Click Next

For Configure stack options we recommend configuring tags, which are key-value pairs, that can help you identify your stacks and the resources they create. For example, enter Owner in the left column which is the key, and your email address in the right column which is the value. We will not use additional permissions or advanced options so click Next. For more information, see Setting AWS CloudFormation Stack Options .

For Review

Review the contents of the page
At the bottom of the page, select I acknowledge that AWS CloudFormation might create IAM resources with custom names
Click Create stack

![image](https://user-images.githubusercontent.com/103466963/205398156-2f0cf220-fc2e-4c3a-a083-5c672eb01cd6.png)

This will take you to the CloudFormation stack status page, showing the stack creation in progress.

Click on the Events tab
Scroll through the listing. It shows the activities performed by CloudFormation (newest events at top), such as starting to create a resource and then completing the resource creation.
Any errors encountered during the creation of the stack will be listed in this tab.


At the bottom of the page, select I acknowledge that AWS CloudFormation might create IAM resources with custom names

When it shows status CREATE_COMPLETE, then you are finished with this step.

You have now set up detective controls to log to your buckets and retain events, giving you the ability to search history and later enable pro-active monitoring of your AWS account!

# NOTE
You should receive an email to confirm the SNS email subscription, you must confirm this. Note as the email is directly from GuardDuty via SNS it will be JSON format.


# KNOWLEDGE CHECK

The security best practices followed in this lab are:

Configure service and application logging AWS Cloudtrail, AWS Config and Amazon GuardDuty provide insights into your environment.
Evaluate and implement new security services and features regularly: New features such as Amazon GuardDuty have been adopted.
Automate testing and validation of security controls in pipelines: CloudFormation is being used to configure AWS CloudTrail, AWS Config and Amazon GuardDuty.
Implement managed services: Managed services are utilized to increase your visibility and control of your environment.


# TEAR DOWN

The following instructions will remove the resources that have a cost for running them.

Note: If you are planning on doing the lab 300_Incident_Response_with_AWS_Console_and_CLI we recommend you only tear down this stack after completing that lab as their is a dependency on AWS CloudTrail being enabled for the other lab.

Delete the stack:

Sign in to the AWS Management Console, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/.
Select the DetectiveControls stack.
Click the Actions button then click Delete Stack.
Confirm the stack and then click the Yes, Delete button.
Empty and delete the S3 buckets:

Sign in to the AWS Management Console, and open the S3 console at https://console.aws.amazon.com/s3/.
Select the CloudTrail bucket name you previously created without clicking the name.

![image](https://user-images.githubusercontent.com/103466963/205398623-cb6066bf-e6fa-4316-b4c2-13d8f67bcb62.png)

Click Empty bucket and enter the bucket name in the confirmation box.

![image](https://user-images.githubusercontent.com/103466963/205398660-3f22e5d4-7d41-4ac5-b8f3-724802357a31.png)

Click Confirm and the bucket will be emptied when the bottom task bar has 0 operations in progress.

![image](https://user-images.githubusercontent.com/103466963/205398705-01f7b3fc-4f09-4325-ad28-63f1652e5dd5.png)

With the bucket now empty, click Delete bucket.

![image](https://user-images.githubusercontent.com/103466963/205398753-c4d36c6e-b135-487d-8dd3-a0a6c65a57c0.png)

Enter the bucket name in the confirmation box and click Confirm.

![image](https://user-images.githubusercontent.com/103466963/205398824-0adc4b6f-eac5-4e1e-ae82-04831225f328.png)

Repeat steps 2 to 6 for the Config bucket you created.



