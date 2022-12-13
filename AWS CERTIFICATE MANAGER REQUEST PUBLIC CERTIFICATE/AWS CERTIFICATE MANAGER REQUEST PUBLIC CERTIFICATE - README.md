# AWS CERTIFICATE MANAGER REQUEST PUBLIC CERTIFICATE

# Introduction

AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources. 
SSL/TLS certificates are used to secure network communications and establish the identity of websites over the Internet as well as resources on private networks. 
AWS Certificate Manager removes the time-consuming manual process of purchasing, uploading, and renewing SSL/TLS certificates.

# Goals
Request AWS Certificate Manager public certificate

# Prerequisites

An AWS account that you are able to use for testing, that is not used for production or other purposes. 
NOTE: You will be billed for any applicable AWS resources used if you complete this lab that are not covered in the AWS Free Tier . See pricing for further information on AWS Certificate Manager.

Steps:
Requesting a public certificate using the console
Tear down



# REQUESTING A PUBLIC CERTIFICATE USING THE CONSOLE

Sign into the AWS Management Console and open the ACM console at https://console.aws.amazon.com/acm/home . Select your prefferred region for regional certificates including Elastic Load Balancing, or US East (N. Virginia) for global services including Amazon CloudFront.

If you see a welcome page, click Get started under provision certificates area.

On the Request a certificate page, click Request a public certificate, then click Request a certificate.

Type your domain name. You can use a fully qualified domain name (FQDN) such as www.example.com or a bare or apex domain name such as example.com. You can also use an asterisk * as a wildcard in the leftmost position to protect several site names in the same domain. For example, *.example.com protects corp.example.com, and images.example.com. The wildcard name will appear in the Subject field and the Subject Alternative Name extension of the ACM certificate.

Note: When you request a wildcard certificate, the asterisk * must be in the leftmost position of the domain name and can protect only one subdomain level. For example, *.example.com can protect login.example.com, and test.example.com, but it cannot protect test.login.example.com. Also note that *.example.com protects only the subdomains of example.com, it does not protect the bare or apex domain example.com. To protect both, see the next step.

To add more domain names to the ACM certificate, choose Add another name to this certificate and type another domain name in the text box that opens. This is useful for protecting both a bare or apex domain (like example.com) and its subdomains *.example.com.

After you have typed valid domain names, choose Next.

Before ACM issues a certificate, it validates that you own or control the domain names in your certificate request. You can use either email validation or DNS validation. If you choose email validation, ACM sends validation email to three contact addresses registered in the WHOIS database and to five common system administration addresses for each domain name. You or an authorized representative must approve one of these email messages. If you use DNS validation, you simply create a CNAME record provided by ACM to your DNS configuration. Choose your option, then click Review.

Note: If you are able to edit your DNS configuration, we recommend that you use DNS domain validation rather than email validation. DNS validation has multiple benefits over email validation. See Use DNS to Validate Domain Ownership.

If the review page correctly contains the information that you provided for your request, choose Confirm and request. The following page shows that your request status is pending validation. You must approve the request either through email link or DNS record.

Important: Unless you choose to opt out, your certificate will be automatically recorded in at least two public certificate transparency databases. You cannot currently use the console to opt out. You must use the AWS CLI or the API. For more information, see Opting Out of Certificate Transparency Logging . For general information about transparency logs, see Certificate Transparency Logging .

Your certificate is now ready to associate with a supported service .

# TEAR DOWN

The following instructions will remove the certificate you have created.

Sign into the AWS Management Console and open the ACM console at https://console.aws.amazon.com/acm/home . Select the region where you created the certificate.
Click the check box for the domain name of the certificate to delete. Click Actions then Delete.
Verify this is the certificate to delete and click Delete. Note: You cannot delete an ACM Certificate that is being used by another AWS service. To delete a certificate that is in use, you must first remove the certificate association.
