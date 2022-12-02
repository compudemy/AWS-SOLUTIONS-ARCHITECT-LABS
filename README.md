# AWS-SOLUTIONS-ARCHITECT-LABS

# ENABLE SECURITY HUB

AWS Security Hub gives you a comprehensive view of your high-priority security alerts and compliance status across AWS accounts. 
There is a range of powerful security tools at your disposal, from firewalls and endpoint protection to vulnerability and compliance scanners. 
But oftentimes this leaves your team switching back-and-forth between these tools to deal with hundreds, and sometimes thousands, of security alerts every day. 
With Security Hub, you now have a single place that aggregates, organizes, and prioritizes your security alerts, or findings, from multiple AWS services, 
such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie, as well as from AWS Partner solutions. Your findings are visually summarized on integrated dashboards with actionable graphs and tables. 
You can also continuously monitor your environment using automated compliance checks based on the AWS best practices and industry standards your organization follows. 
Get started with AWS Security Hub in just a few clicks in the Management Console and once enabled, Security Hub will begin aggregating and prioritizing findings.

# Prerequisites
An AWS account that you are able to use for testing, that is not used for production or other purposes.

# Costs
Typically less than $1 per month if the account is only used for personal testing or training, and the tear down is not performed.
AWS Config Pricing
AWS Security Hub pricing
AWS Pricing

# Steps:
Enable AWS Security Hub
Tear Down


# ENABLE AWS SECURITY HUB

Table of Contents
Getting Started
1. Getting Started
The AWS console provides a graphical user interface to search and work with the AWS services. 
We will use the AWS console to enable AWS Security Hub.

# 1.1 Enable AWS Config

AWS Security Hub requires AWS Config to run within your account.

If you have not enabled AWS Config, we’ll need to enable that now. 
If it’s already enabled in your account, you can skip to the next step. Navigate to the AWS Config console and select 1-click setup and then select Confirm.

![image](https://user-images.githubusercontent.com/103466963/205345977-1d3dcedd-9d9d-483f-a64b-34c03443e53a.png)

Once successful, you’ll see this Welcome to AWS Config page.
![image](https://user-images.githubusercontent.com/103466963/205346202-be65ca5b-ff66-4239-9bfe-0d6958913831.png)

# 1.2 AWS Security Hub

Once you have logged into your AWS account and enabled AWS Config, we need to enable Security Hub. 
Navigate to the AWS Security Hub console .

Alternatively, you can just search for Security Hub and select the service.
![image](https://user-images.githubusercontent.com/103466963/205346449-f2dd2d92-4690-4f17-9e28-51cd9da3fe89.png)

# 1.3 Enable AWS Security Hub

In the AWS Security Hub service console you can click on the Go to Security Hub orange button to navigate to AWS Security Hub in your account.

![image](https://user-images.githubusercontent.com/103466963/205346592-c011f04a-e1d0-4c7f-8a24-aee81ee171cd.png)

Additional information is provided regarding Security standards and AWS Integrations. You can read more here . 
Now select Enable Security Hub.

![image](https://user-images.githubusercontent.com/103466963/205346930-a9e37d2a-96c8-421d-ba2f-a5f157be2891.png)

# 1.4 Explore AWS Security Hub

NOTE: Because Security Hub is a Regional service, the checks performed for this control only apply to the current Region for the account. It must be enabled separately for each region.

With AWS Security Hub now enabled in your account, you can explore the security insights AWS Security Hub offers.

![image](https://user-images.githubusercontent.com/103466963/205347039-4692d556-4aaa-4e4c-9eb7-fb027d0a6dfb.png)

Once you enable, it may take up to two hours or more to see results from the security checks. You might see this banner below.

![image](https://user-images.githubusercontent.com/103466963/205347110-5cbb9c61-f66d-4a18-b535-6edac6068bfe.png)

If you forgot to enable AWS Config, you might see this banner.

![image](https://user-images.githubusercontent.com/103466963/205347160-bd0ed877-5d8d-4e10-88a7-80aa0c59158f.png)

