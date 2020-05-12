# Transferring a domain to a different AWS account<a name="domain-transfer-between-aws-accounts"></a>

If you registered a domain using one AWS account and you want to transfer the domain to another AWS account, you can contact the AWS Support Center and request the transfer\. They can also help if the AWS account that the domain is registered with is closed, suspended, or terminated\.

Alternatively, you can transfer the domain between AWS accounts yourself using the AWS CLI or other programmatic methods\.

**Topics**
+ [Step 1: Transfer a domain to a different AWS account](#domain-transfer-between-aws-accounts-domain)
+ [Step 2 \(Optional\): Migrate a hosted zone to a different AWS account](#domain-transfer-between-aws-accounts-hosted-zone)

## Step 1: Transfer a domain to a different AWS account<a name="domain-transfer-between-aws-accounts-domain"></a>

When you want to transfer a domain from one AWS account to another, you have two options:

**Transfer the domain yourself**  
You can transfer the domain yourself programmatically, using the AWS CLI, one of the AWS SDKs, or the Route 53 API\. See the following documentation:  
+ For an overview of the transfer process and documentation about the API actions that you use to transfer a domain using the Route 53 domain registration API, see [TransferDomainToAnotherAwsAccount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_TransferDomainToAnotherAwsAccount.html) in the *Amazon Route 53 API Reference*\.
+ For documentation about other options for transferring domains programmatically, see "SDKs & Toolkits" in the [Guides and API References](https://docs.aws.amazon.com/#user_guides) section of the "AWS documentation" page\.

**Contact AWS Support**  
You can work with AWS Support to transfer the domain\. See the following procedure\.

**Important**  
When you transfer a domain to a different AWS account, either with help from AWS Support or programmatically, the hosted zone for the domain isn't transferred\. If you also want to transfer the hosted zone, wait until the domain has been transferred, and then see [Step 2 \(Optional\): Migrate a hosted zone to a different AWS account](#domain-transfer-between-aws-accounts-hosted-zone)\. <a name="domain-transfer-between-aws-accounts-procedure"></a>

**To work with AWS Support to transfer a domain to a different AWS account**

1. Using the AWS account that the domain is currently registered to, sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\.
**Important**  
You must sign in either by using the root account or by using an IAM user that has been granted IAM permissions in one or more of the following ways:  
The user is assigned the **AdministratorAccess** managed policy\.
The user is assigned the **AmazonRoute53DomainsFullAccess** managed policy\.
The user is assigned the **AmazonRoute53FullAccess** managed policy\.
The user is assigned the **PowerUserAccess** managed policy\.
The user has permission to perform all the following actions: `TransferDomains`, `DisableDomainTransferLock`, and `RetrieveDomainAuthCode`\.
If you don't sign in either by using the root account or by using an IAM user that has the required permissions, we can't perform the transfer\. This requirement prevents unauthorized users from transferring domains to other AWS accounts\.

1. Specify the following values\. The form automatically fills in the first three values:  
***Option buttons directly below* Create case**  
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

## Step 2 \(Optional\): Migrate a hosted zone to a different AWS account<a name="domain-transfer-between-aws-accounts-hosted-zone"></a>

If you're using Route 53 as the DNS service for the domain, Route 53 doesn't transfer the hosted zone when you transfer a domain to a different AWS account\. If domain registration is associated with one account and the corresponding hosted zone is associated with another account, neither domain registration nor DNS functionality is affected\. The only effect is that you'll need to sign into the Route 53 console using one account to see the domain, and sign in using the other account to see the hosted zone\. 

If you own the account that you're transferring the domain from and the account that you're transferring the domain to, you can optionally migrate the hosted zone for the domain to a different account, but it's not required\. Route 53 will continue to use the records in the existing hosted zone to route traffic for the domain\.

**Important**  
If you don't own both the account that you're transferring the domain from and the account that you're transferring the domain to, you must either migrate the existing hosted zone to the AWS account that you're transferring the domain to, or create a new hosted zone in an AWS account that you own\. If you don't own the account that created the hosted zone that routes traffic for the domain, you can't control how traffic is routed\.

To migrate the existing hosted zone to the new account, see [Migrating a hosted zone to a different AWS account](hosted-zones-migrating.md)\.

To create a new hosted zone, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\. This topic is typically used when you're transferring domains from another registrar to Route 53, but the process is the same when you're transferring domains from one AWS account to another\.