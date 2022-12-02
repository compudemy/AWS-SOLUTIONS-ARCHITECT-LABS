# AWS-SOLUTIONS-ARCHITECT-LABS

ENABLE SECURITY HUB

AWS Security Hub gives you a comprehensive view of your high-priority security alerts and compliance status across AWS accounts. 
There is a range of powerful security tools at your disposal, from firewalls and endpoint protection to vulnerability and compliance scanners. 
But oftentimes this leaves your team switching back-and-forth between these tools to deal with hundreds, and sometimes thousands, of security alerts every day. 
With Security Hub, you now have a single place that aggregates, organizes, and prioritizes your security alerts, or findings, from multiple AWS services, 
such as Amazon GuardDuty, Amazon Inspector, and Amazon Macie, as well as from AWS Partner solutions. Your findings are visually summarized on integrated dashboards with actionable graphs and tables. 
You can also continuously monitor your environment using automated compliance checks based on the AWS best practices and industry standards your organization follows. 
Get started with AWS Security Hub in just a few clicks in the Management Console and once enabled, Security Hub will begin aggregating and prioritizing findings.

Prerequisites
An AWS account that you are able to use for testing, that is not used for production or other purposes.

Costs
Typically less than $1 per month if the account is only used for personal testing or training, and the tear down is not performed.
AWS Config Pricing
AWS Security Hub pricing
AWS Pricing

Steps:
Enable AWS Security Hub
Tear Down


ENABLE AWS SECURITY HUB

Table of Contents
Getting Started
1. Getting Started
The AWS console provides a graphical user interface to search and work with the AWS services. 
We will use the AWS console to enable AWS Security Hub.

1.1 Enable AWS Config
AWS Security Hub requires AWS Config to run within your account.

If you have not enabled AWS Config, we’ll need to enable that now. 
If it’s already enabled in your account, you can skip to the next step. Navigate to the AWS Config console and select 1-click setup and then select Confirm.

https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/enable-aws-config.png

Once successful, you’ll see this Welcome to AWS Config page.
https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/aws-config-success.png

1.2 AWS Security Hub
Once you have logged into your AWS account and enabled AWS Config, we need to enable Security Hub. 
Navigate to the AWS Security Hub console .

Alternatively, you can just search for Security Hub and select the service.
https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/search-for-security-hub.png

1.3 Enable AWS Security Hub
In the AWS Security Hub service console you can click on the Go to Security Hub orange button to navigate to AWS Security Hub in your account.

https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/go-to-security-hub.png

Additional information is provided regarding Security standards and AWS Integrations. You can read more here . 
Now select Enable Security Hub.

https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/enable-security-hub.png


1.4 Explore AWS Security Hub
NOTE: Because Security Hub is a Regional service, the checks performed for this control only apply to the current Region for the account. It must be enabled separately for each region.

With AWS Security Hub now enabled in your account, you can explore the security insights AWS Security Hub offers.
https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/explore-aws-security-hub.png

Once you enable, it may take up to two hours or more to see results from the security checks. You might see this banner below.
https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/after-security-hub-enable.png

If you forgot to enable AWS Config, you might see this banner.
https://www.wellarchitectedlabs.com/Security/100_Enable_Security_Hub/Images/aws-config-error.png


