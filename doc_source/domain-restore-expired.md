# Restoring an Expired Domain<a name="domain-restore-expired"></a>

If you don't renew a domain before the end of the late\-renewal period or if you accidentally delete the domain, some registries for top\-level domains \(TLDs\) allow you to restore the domain before it becomes available for others to register\.

When a domain is deleted or it passes the end of the late\-renewal period, it no longer appears in the Amazon Route 53 console\. 

**Important**  
The price for restoring a domain is typically higher and sometimes much higher than the price for registering or renewing a domain\. For the current price for restoring a domain, see the "Restoration Price" column in [Amazon Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\.

**To try to restore domain registration when a domain is deleted or the late\-renewal period has expired**

1. Determine whether the TLD registry for the domain supports restoring domains and, if so, the period during which restoration is allowed\.

   1. Go to the "Renewal, restoration, and deletion times" table on the [Renewing a Domain Name](http://wiki.gandi.net/en/domains/renew) page on the Gandi website\.

   1. Find the TLD for your domain, and review the values in the **Restoration possible** column\. 
**Important**  
We forward restoration requests to Gandi, which processes the requests during business hours Monday through Friday\. Gandi is based in Paris, where the time is UTC/GMT \+1 hour\. As a result, depending on when you submit your request, in rare cases it can take a week or more for a request to be processed\.

1. Using the AWS account that the domain was registered to, sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\. 

1. Specify the following values:  
**Regarding**  
Accept the default value of **Account and Billing Support**\.  
**Service**  
Accept the default value of **Billing**\.  
**Category**  
Accept the default value of **Domain name registration issue**\.  
**Subject**  
Type **Restore an expired domain** or **Restore a deleted domain**\.  
**Description**  
Provide the following information:  

   + The domain that you want to restore

   + The [12\-digit account ID](http://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html#FindingYourAccountIdentifiers) of the AWS account that the domain was registered to  
**Contact method**  
Specify a contact method and, if you choose **Phone**, enter the applicable values\.

1. Choose **Submit**\.

1. When we learn whether we were able to restore your domain, a customer support representative will contact you\. In addition, if we were able to restore your domain, the domain will reappear in the console with the new expiration date\. 