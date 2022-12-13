# AUTOMATED DEPLOYMENT OF IAM GROUPS AND ROLES 

# Introduction

This hands-on lab will guide you through how to use AWS CloudFormation to automatically configure AWS Identity and Access Management (IAM) Groups and roles for cross-account access. 
You will use the AWS Management Console and AWS CloudFormation to guide you through how to automate the configuration of a new or existing AWS account with IAM best practices. 
The skills you learn will help you secure your workloads in alignment with the AWS Well-Architected Framework .

# Goals

Fine-grained authorization
Automate security best practices

# Prerequisites

An AWS account that you are able to use for testing.
Permissions to create resources in IAM.

# Costs
There are no costs for this lab
AWS Pricing

# Steps:
AWS CloudFormation to Create Groups, Policies and Roles with MFA Enforced
Assume Roles from an IAM user

# Tear down

# AWS CLOUDFORMATION TO CREATE GROUPS, POLICIES AND ROLES WITH MFA ENFORCED

# 1.1 Create AWS CloudFormation Stack
Sign in to the AWS Management Console, select your preferred region, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/.
Click Create stack.

![image](https://user-images.githubusercontent.com/103466963/206700904-0a5539d1-7641-48d8-ae13-c72da919df8b.png)

Enter the following Amazon S3 URL: https://s3-us-west-2.amazonaws.com/aws-well-architected-labs/Security/Code/baseline-iam.yaml and click Next.

![image](https://user-images.githubusercontent.com/103466963/206701005-ea9461be-4c97-4738-be11-ca301f4471c1.png)

Enter the following details:
Stack name: The name of this stack. For this lab, use baseline-iam.
AllowRegion: A single region to restrict access, enter your preferred region.
BaselineExportName: The CloudFormation export name prefix used with the resource name for the resources created, for example, Baseline-PrivilegedAdminRole.
BaselineNamePrefix: The prefix for roles, groups, and policies created by this stack.
IdentityManagementAccount: (optional) AccountId that contains centralized IAM users and is trusted to assume all roles, or blank for no cross-account trust. Note that the trusted account needs to be appropriately secured.
OrganizationsRootAccount: (optional) AccountId that is trusted to assume Organizations role, or blank for no cross-account trust. Note that the trusted account needs to be appropriately secured.
ToolingManagementAccount: AccountId that is trusted to assume the ReadOnly and StackSet roles, or blank for no cross-account trust. Note that the trusted account needs to be appropriately secured.
At the bottom of the page click Next.
In this lab, we won’t add any tags or other options. Click Next. Tags, which are key-value pairs, can help you identify your stacks. For more information, see Adding Tags to Your AWS CloudFormation Stack .
Review the information for the stack. When you’re satisfied with the configuration, check I acknowledge that AWS CloudFormation might create IAM resources with custom names then click Create stack.

![image](https://user-images.githubusercontent.com/103466963/206701101-2290b548-3f2c-4691-8b28-482ee0764a29.png)

After a few minutes the stack status should change from CREATE_IN_PROGRESS to CREATE_COMPLETE.
You have now set up a number of managed polices, groups, and roles that you can test to improve your AWS security!


# ASSUME ROLES FROM AN IAM USER

We will assume the roles previously created in the web console and command line interface (CLI) using an existing IAM user.

2.1 Use Restricted Administrator Role in Web Console
A role specifies a set of permissions that you can use to access AWS resources that you need. In that sense, it is similar to a user in AWS Identity and Access Management (IAM). A benefit of roles is they allow you to enforce the use of an MFA token to help protect your credentials. When you sign in as a user, you get a specific set of permissions. However, you don’t sign in to a role, but once signed in (as a user) you can switch to a role. This temporarily sets aside your original user permissions and instead gives you the permissions assigned to the role. The role can be in your own account or any other AWS account. By default, your AWS Management Console session lasts for one hour.

Important

The permissions of your IAM user and any roles that you switch to are not cumulative. 
Only one set of permissions is active at a time. When you switch to a role, 
you temporarily give up your user permissions and work with the permissions that are assigned to the role. 
When you exit the role, your user permissions are automatically restored.

Sign in to the AWS Management Console as an IAM user https://console.aws.amazon.com .

In the console, click your user name on the navigation bar in the upper right. It typically looks like this: username@account_ID_number_or_alias. Alternatively you can paste the link in your browser that you recorded earlier.

Click Switch Role. If this is the first time choosing this option, a page appears with more information. After reading it, click Switch Role. If you clear your browser cookies, this page can appear again.

On the Switch Role page, type the account ID number or the account alias and the name of the role that you created for the Administrator in the previous step, for example, arn:aws:iam::account_ID:role/Administrator.

(Optional) Type text that you want to appear on the navigation bar in place of your user name when this role is active. A name is suggested, based on the account and role information, but you can change it to whatever has meaning for you. You can also select a color to highlight the display name. The name and color can help remind you when this role is active, which changes your permissions. For example, for a role that gives you access to the test environment, you might specify a Display Name of Test and select the green Color. For the role that gives you access to production, you might specify a Display Name of Production and select red as the Color.

Click Switch Role. The display name and color replace your user name on the navigation bar, and you can start using the permissions that the role grants you.

Tip

The last several roles that you used appear on the menu. The next time you need to switch to one of those roles, you can simply choose the role you want. You only need to type the account and role information manually if the role is not displayed on the Identity menu.

You are now using the role with the granted permissions! To stop using a role In the IAM console, choose your role’s Display Name on the right side of the navigation bar. Choose Back to UserName. The role and its permissions are deactivated, and the permissions associated with your IAM user and groups are automatically restored.

2.2 Use Restricted Administrator Role in Command Line Interface (CLI)

Coming soon, for now check out: https://docs.aws.amazon.com/cli/latest/userguide/cli-roles.html


# TEAR DOWN

The following instructions will remove the resources that have a cost for running them. Please note that the changes you made to the root login, users, groups, and policies have no charges associated with them.

Delete the IAM stack:

Sign in to the AWS Management Console, and open the CloudFormation console at https://console.aws.amazon.com/cloudformation/.
Select the baseline-iam stack.
Click the Actions button then click Delete Stack.
Confirm the stack and then click the Yes, Delete button.





