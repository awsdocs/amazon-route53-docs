# Transferring a domain to a different AWS account<a name="domain-transfer-between-aws-accounts"></a>

If you registered a domain using one AWS account and you want to transfer the domain to another AWS account, you can transfer it by using the console, or by using the AWS CLI or other programmatic methods\. Before you transfer a domain to another AWS account, turn off the transfer lock\. For more information, see [Locking a domain to prevent unauthorized transfer to another registrar](domain-lock.md)\.

**Topics**
+ [Step 1: Transfer a domain to a different AWS account](#domain-transfer-between-aws-accounts-domain)
+ [Step 2 \(Optional\): Migrate a hosted zone to a different AWS account](#domain-transfer-between-aws-accounts-hosted-zone)

## Step 1: Transfer a domain to a different AWS account<a name="domain-transfer-between-aws-accounts-domain"></a>

When you want to transfer a domain from one AWS account to another, you have two options:

**Use the new console to transfer the domain**  
Use the [initiate a transfer to another AWS account](#domain-transfer-between-aws-accounts-procedure) and [accept a transfer from another AWS account](#domain-transfer-between-aws-accounts-accept-procedure) procedures\.

**Transfer the domain programmatically**  
You can transfer the domain yourself programmatically, using the AWS CLI, one of the AWS SDKs, or the Route 53 API\. See the following documentation:  
+ For an overview of the transfer process and documentation about the API actions that you use to transfer a domain using the Route 53 domain registration API, see [TransferDomainToAnotherAwsAccount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_TransferDomainToAnotherAwsAccount.html) in the *Amazon Route 53 API Reference*\.
+ For documentation about other options for transferring domains programmatically, see "SDKs & Toolkits" in the [Guides and API References](https://docs.aws.amazon.com/#user_guides) section of the "AWS documentation" page\.
+ The receiving account has three days to accept the transfer from the originating account, by using the [transfer\-domain\-to\-another\-aws\-account](https://docs.aws.amazon.com/cli/latest/reference/route53domains/transfer-domain-to-another-aws-account.html) API\. If the transfer isn't accepted in three days, the transfer request is cancelled\.
**Important**  
When you transfer a domain to a different AWS account programmatically, the hosted zone for the domain isn't transferred\. If you also want to transfer the hosted zone, wait until the domain has been transferred, and then see [Step 2 \(Optional\): Migrate a hosted zone to a different AWS account](#domain-transfer-between-aws-accounts-hosted-zone)\. 

Whether you transfer the domain on the new console, or programmatically, you must sign in either by using the root account or by using a user that has been granted IAM permissions in one or more of the following ways:
+ The user is assigned the **AdministratorAccess** managed policy\.
+ The user is assigned the **AmazonRoute53DomainsFullAccess** managed policy\.
+ The user is assigned the **AmazonRoute53FullAccess** managed policy\.
+ The user is assigned the **PowerUserAccess** managed policy\.
+ The user has permission to perform all the following actions: `TransferDomains`, `DisableDomainTransferLock`, and `RetrieveDomainAuthCode`\.

If you don't sign in either by using the root account or by using a user that has the required permissions, we can't perform the transfer\. This requirement prevents unauthorized users from transferring domains to other AWS accounts\.

**Note**  
We're updating the domains console for Route 53\. The following procedures for transferring and accepting a domain transfer between AWS account can be completed on the new console\.<a name="domain-transfer-between-aws-accounts-procedure"></a>

**To transfer a domain to a different AWS account**

1. Sign in to AWS by using the AWS account that the domain is currently registered to\. 

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered domains**\.

1. Choose the name of the domain that you want to transfer to another AWS account\.

1. Above the **Details** section, in the **Transfer out** dropdown, choose **Transfer to another AWS account**\.

1. On the **Transfer to another AWS account** dialog, enter the destination account ID\. You can get this ID from the destination AWS account owner\.

1. Choose **Confirm**\.

1. On the **Generate password** dialog, copy the password, and forward it to the receiving AWS account owner\.

   On the **Requests** page, the **Status** for the domain will display **In progress**, and the **Type** will display **Internal transfer out**\.<a name="domain-transfer-between-aws-accounts-accept-procedure"></a>

**To accept a domain transfer from a different AWS account**

1. Sign into AWS by using the AWS account that is receiving the domain\. 

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Requests**\.

1. On the **Requests** page, select the radio button next to the domain name you are transferring from another AWS account\. If the domain is ready to be transferred the **Status** is **Action required** and the **Type** is **Internal transfer of domain in**\.

   You have three days to accept the request\. If the transfer isn't accepted in three days, the transfer request is cancelled\.

1. In the **Action** dropdown, choose **Accept**\.

   You can also choose **Reject** to cancel the transfer process\.

1. If you accepted, on the **Transfer domain to your account** page, in the **Password** section, enter the password you received from the originating account owner\. 

   Accept the terms and conditions, and choose **Next**\.

1. Navigate to the **Requests** page to monitor the transfer status and other steps to complete\.

1. After the transfer completes, you can update the contact information\. For more information, see [Updating contact information and ownership for a domain](domain-update-contacts.md)\.



## Step 2 \(Optional\): Migrate a hosted zone to a different AWS account<a name="domain-transfer-between-aws-accounts-hosted-zone"></a>

If you're using Route 53 as the DNS service for the domain, Route 53 doesn't transfer the hosted zone when you transfer a domain to a different AWS account\. If domain registration is associated with one account and the corresponding hosted zone is associated with another account, neither domain registration nor DNS functionality is affected\. The only effect is that you'll need to sign into the Route 53 console using one account to see the domain, and sign in using the other account to see the hosted zone\. 

If you own the account that you're transferring the domain from and the account that you're transferring the domain to, you can optionally migrate the hosted zone for the domain to a different account, but it's not required\. Route 53 will continue to use the records in the existing hosted zone to route traffic for the domain\.

**Important**  
If you don't own both the account that you're transferring the domain from and the account that you're transferring the domain to, you must either migrate the existing hosted zone to the AWS account that you're transferring the domain to, or create a new hosted zone in an AWS account that you own\. If you don't own the account that created the hosted zone that routes traffic for the domain, you can't control how traffic is routed\.

To migrate the existing hosted zone to the new account, see [Migrating a hosted zone to a different AWS account](hosted-zones-migrating.md)\.

To create a new hosted zone, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\. This topic is typically used when you're transferring domains from another registrar to Route 53, but the process is the same when you're transferring domains from one AWS account to another\.