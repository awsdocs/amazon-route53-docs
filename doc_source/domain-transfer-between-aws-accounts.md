# Transferring a Domain to a Different AWS Account<a name="domain-transfer-between-aws-accounts"></a>

If you registered a domain using one AWS account and you want to transfer the domain to another AWS account, you can do so by contacting the AWS Support Center and requesting the transfer\.

**Topics**
+ [Step 1: Transferring a Domain to a Different AWS Account](#domain-transfer-between-aws-accounts-domain)
+ [Step 2: Migrating a Hosted Zone to a Different AWS Account](#domain-transfer-between-aws-accounts-hosted-zone)

## Step 1: Transferring a Domain to a Different AWS Account<a name="domain-transfer-between-aws-accounts-domain"></a>

To transfer registration for a domain from one AWS account to another, perform the following procedure\.

**Important**  
When someone in AWS Support transfers a domain to a different AWS account for you, they aren't able to transfer the hosted zone for the domain\. If you also want to transfer the hosted zone, wait until the domain has been transferred, and then see [Step 2: Migrating a Hosted Zone to a Different AWS Account](#domain-transfer-between-aws-accounts-hosted-zone)\. <a name="domain-transfer-between-aws-accounts-procedure"></a>

**To transfer a domain to a different AWS account**

1. Using the AWS account that the domain is currently registered to, sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\.
**Important**  
You must sign in either by using the root account or by using an IAM user that has been granted IAM permissions in one or more of the following ways:  
The user is assigned the **AdministratorAccess** managed policy\.
The user is assigned the **AmazonRoute53DomainsFullAccess** managed policy\.
The user is assigned the **AmazonRoute53FullAccess** managed policy\.
The user has permission to perform all the following actions: `TransferDomains`, `DisableDomainTransferLock`, and `RetrieveDomainAuthCode`\.
If you don't sign in either by using the root account or by using an IAM user that has the required permissions, we can't perform the transfer\. This requirement prevents unauthorized users from transferring domains to other AWS accounts\.

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
   + [12\-digit account ID](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html#FindingYourAccountIdentifiers) of the AWS account that the domain is currently registered to
   + [12\-digit account ID](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html#FindingYourAccountIdentifiers) of the AWS account that you want to transfer domain registration to  
**Contact method**  
Choose a contact method, **Web** or **Phone**\. If you choose **Web**, we'll contact you using the email address that's associated with your AWS account\. If you choose **Phone**, enter the applicable values\.

1. Choose **Submit**\.

## Step 2: Migrating a Hosted Zone to a Different AWS Account<a name="domain-transfer-between-aws-accounts-hosted-zone"></a>

If you're using Route 53 as the DNS service for the domain, Route 53 doesn't transfer the hosted zone when you transfer a domain to a different AWS account\. If domain registration is associated with one account and the corresponding hosted zone is associated with another account, neither domain registration nor DNS functionality is affected\. The only effect is that you'll need to sign into the Route 53 console using one account to see the domain, and sign in using the other account to see the hosted zone\. 

If you own the account that you're transferring the domain from and the account that you're transferring the domain to, you can optionally migrate the hosted zone for the domain to a different account, but it's not required\. Route 53 will continue to use the records in the existing hosted zone to route traffic for the domain\.

**Important**  
If you don't own both the account that you're transferring the domain from and the account that you're transferring the domain to, you must either migrate the existing hosted zone to the AWS account that you're transferring the domain to, or create a new hosted zone in an AWS account that you own\. If you don't own the account that created the hosted zone that routes traffic for the domain, you can't control how traffic is routed\.

To migrate the existing hosted zone to the new account, see [Migrating a Hosted Zone to a Different AWS Account](hosted-zones-migrating.md)\.

To create a new hosted zone, see [Making Amazon Route 53 the DNS Service for an Existing DomainMaking Route 53 the DNS Service for an Existing Domain](MigratingDNS.md)\. This topic is typically used when you're transferring domains from another registrar to Route 53, but the process is the same when you're transferring domains from one AWS account to another\.