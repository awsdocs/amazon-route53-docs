# Transferring a Domain to a Different AWS Account<a name="domain-transfer-between-aws-accounts"></a>

If you registered a domain using one AWS account and you want to transfer the domain to another AWS account, you can do so by contacting the AWS Support Center and requesting the transfer\.


+ [Step 1: Transferring a Domain to a Different AWS Account](#domain-transfer-between-aws-accounts-domain)
+ [Step 2: \(Optional\) Migrating a Hosted Zone to a Different AWS Account](#domain-transfer-between-aws-accounts-hosted-zone)

## Step 1: Transferring a Domain to a Different AWS Account<a name="domain-transfer-between-aws-accounts-domain"></a>

To transfer registration for a domain from one AWS account to another, perform the following procedure\.

**To transfer a domain to a different AWS account**

1. Using the AWS account that the domain is currently registered to, sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\.
**Important**  
You must sign in by using the root account that the domain is currently registered to\. If you sign in by using an IAM user or any other account, we can't perform the transfer\. This requirement prevents unauthorized users from transferring domains to other AWS accounts\.

1. Specify the following values:  
**Regarding**  
Accept the default value of **Account and Billing Support**\.  
**Service**  
Accept the default value of **Billing**\.  
**Category**  
Accept the default value of **Domain name registration issue**\.  
**Subject**  
Specify **Transfer a domain to another AWS account**\.  
**Description**  
Provide the following information:  

   + Domain that you want to transfer

   + Account ID of the AWS account that the domain is currently registered to

   + Account ID of the AWS account that you want to transfer domain registration to  
**Contact method**  
Specify a contact method and, if you choose **Phone**, enter the applicable values\.

1. Choose **Submit**\.

## Step 2: \(Optional\) Migrating a Hosted Zone to a Different AWS Account<a name="domain-transfer-between-aws-accounts-hosted-zone"></a>

If you're using Route 53 as the DNS service for the domain, Route 53 doesn't transfer the hosted zone when you transfer a domain to a different AWS account\. If domain registration is associated with one account and the corresponding hosted zone is associated with another account, neither domain registration nor DNS functionality is affected\. The only effect is that you'll need to sign into the Route 53 console using one account to see the domain, and sign in using the other account to see the hosted zone\. 

You can optionally transfer the hosted zone for the domain to a different account, too\. For more information, see [Migrating a Hosted Zone to Another AWS Account](hosted-zones-migrating.md)\.