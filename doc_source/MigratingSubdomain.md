# Migrating DNS Service for a Subdomain to Amazon Route 53 without Migrating the Parent Domain<a name="MigratingSubdomain"></a>

You can migrate a subdomain to use Amazon Route 53 as the DNS service without migrating the parent domain from another DNS service\.

The process has four basic steps:

1. Create an Amazon Route 53 hosted zone for the subdomain\.

1. Get the current DNS configuration from the current DNS service provider for the parent domain\.

1. Add resource record sets for the subdomain to your Amazon Route 53 hosted zone\.

1. *API only:* Confirm that your changes have propagated to all Amazon Route 53 DNS servers\.
**Note**  
Currently, the only way to verify that changes have propagated is to use the [GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API action\. Changes generally propagate to all Amazon Route 53 name servers within 60 seconds\.

1. Update the DNS configuration with the DNS service provider for the parent domain by adding name server records for the subdomain\.

## Creating a Hosted Zone for the Subdomain<a name="CreateZoneMigratedSubdomain"></a>

If you want to migrate a subdomain from another DNS service to Amazon Route 53 but you don't want to migrate the parent domain, start by creating a hosted zone for the subdomain\. Amazon Route 53 stores information about your subdomain in the hosted zone\. 

When you create a hosted zone, Amazon Route 53 automatically creates four name server \(NS\) records and a start of authority \(SOA\) record for the zone\. The NS records identify the name servers that you give to your registrar or your DNS service so that queries are routed to Amazon Route 53 name servers\. For more information about NS and SOA records, see [NS and SOA Resource Record Sets that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)\.

To create a hosted zone using the Amazon Route 53 console, perform the following procedure\. To create a hosted zone using the Amazon Route 53 API, use the `CreateHostedZone` action\. For more information, see [CreateHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html) in the *Amazon Route 53 API Reference*\.

**To create a hosted zone using the Amazon Route 53 console**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Amazon Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Amazon Route 53, choose **Hosted Zones** in the **navigation** pane\.

1. In the right pane, enter the name of the subdomain, such as **apex\.example\.com**\. You can also enter an optional comment\. For more information about a field, see the tool tip for the field\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

1. Below the right pane, choose **Create Hosted Zone**\.

## Getting Your Current DNS Configuration from Your DNS Service Provider<a name="GetParentDomainResourceRecords"></a>

To simplify the process of migrating an existing subdomain to Amazon Route 53, get the current DNS configuration for the domain from the DNS service provider that is currently servicing the domain\. You can use this information as a basis for configuring Amazon Route 53 as the DNS service for the subdomain\. 

What you ask for and the format that it comes in depends on which company you're currently using as your DNS service provider\. Ideally, they'll give you a zone file, which contains information about all of the resource record sets in your current configuration\. \(Resource record sets tell DNS how you want traffic to be routed for your domains and subdomains\. For example, when someone enters your domain name in a web browser, do you want traffic to be routed to a web server in your data center, to an Amazon EC2 instance, to a CloudFront distribution, or to some other location?\) If you can get a zone file from your current DNS service provider, you can edit the zone file to remove the resource record sets that you don't want to migrate to Amazon Route 53\. Then you can import the remaining resource record sets into your Amazon Route 53 hosted zone, which greatly simplifies the process\. Try asking customer support for your current DNS service provider how to get a *zone file* or a *records list*\.

## Creating Resource Record Sets<a name="AddMigratedSubdomainRecords"></a>

Using the resource record sets that you got from your current DNS service provider as a starting point, create corresponding resource record sets in the Amazon Route 53 hosted zone that you created for the subdomain\. The resource record sets that you create in Amazon Route 53 will become the resource record sets that DNS uses after you delegate responsibility for the subdomain to Amazon Route 53, as explained in [Updating Your DNS Service with Name Server Records for the Subdomain](#UpdateOldDNS), later in the process\.

**Important**  
Do not create additional name server \(NS\) or start of authority \(SOA\) records in the Amazon Route 53 hosted zone, and do not delete the existing NS and SOA records\. 

To create resource record sets using the Amazon Route 53 console, see [Working with Resource Record Sets](rrsets-working-with.md)\. To create resource record sets using the Amazon Route 53 API, use `ChangeResourceRecordSets`\. For more information, see [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *[Amazon Route 53 API Reference](http://docs.aws.amazon.com/Route53/latest/APIReference/)*\.

## Checking the Status of Your Changes \(API Only\)<a name="MigratingSubdomainCheckStatus"></a>

Creating a new hosted zone and changing resource record sets take time to propagate to the Amazon Route 53 DNS servers\. If you used [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) to create your resource record sets, you can use the `GetChange` action to determine whether your changes have propagated\. \(`ChangeResourceRecordSets` returns a value for `ChangeId`, which you can include in a subsequent `GetChange` request\. `ChangeId` is not available if you created the resource record sets by using the console\.\) For more information, see [GET GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) in the *Amazon Route 53 API Reference*\.

**Note**  
Changes generally propagate to all Amazon Route 53 name servers within 60 seconds\.

## Updating Your DNS Service with Name Server Records for the Subdomain<a name="UpdateOldDNS"></a>

After your changes to Amazon Route 53 resource record sets have propagated \(see [Checking the Status of Your Changes \(API Only\)](#MigratingSubdomainCheckStatus)\), update the DNS service for the parent domain by adding NS records for the subdomain\. This is known as delegating responsibility for the subdomain to Amazon Route 53\. For example, suppose the parent domain example\.com is hosted with another DNS service and you're migrating the subdomain test\.example\.com to Amazon Route 53\. You must create a hosted zone for test\.example\.com and update the DNS service for example\.com with the NS records that Amazon Route 53 assigned to the new hosted zone for test\.example\.com\. 

Perform the following procedure\.

1. Using the method provided by your DNS service, back up the zone file for the parent domain\.

1. If the previous DNS service provider for the domain has a method to change the TTL settings for their name servers, we recommend that you change the settings to 900 seconds\. This limits the time during which client requests will try to resolve domain names using obsolete name servers\. If the current TTL is 172800 seconds \(two days\), which is a common default setting, you still need to wait two days for resolvers and clients to stop caching DNS records using the previous TTL\. After the TTL settings expire, you can safely delete the records that are stored at the previous provider and make changes only to Amazon Route 53\.

1. In the Amazon Route 53 console, get the name servers for your Amazon Route 53 hosted zone:

   1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, click **Hosted Zones**\.

   1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.

   1. In the right pane, make note of the four servers listed for **Name Servers**\.

   Alternatively, you can use the `GetHostedZone` action\. For more information, see [GetHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html) in the *Amazon Route 53 API Reference*\.

1. Using the method provided by the DNS service of the parent domain, add NS records for the subdomain to the zone file for the parent domain\. Give the NS records the same name as the subdomain\. For the values in the NS records, specify the four Amazon Route 53 name servers that are associated with the hosted zone that you created in Step 2\. Note that different DNS services use different terminology\. You might need to contact technical support for your DNS service to learn how to perform this step\. 
**Important**  
Do not add a start of authority \(SOA\) record to the zone file for the parent domain\. Because the subdomain will use Amazon Route 53, the DNS service for the parent domain is not the authority for the subdomain\.   
If your DNS service automatically added an SOA record for the subdomain, delete the record for the subdomain\. However, do not delete the SOA record for the parent domain\.

   Depending on the TTL settings for the name servers for the parent domain, the propagation of your changes to DNS resolvers can take 48 hours or more\. During this period, DNS resolvers may still answer requests with the name servers for the DNS service of the parent domain\. In addition, client computers may continue to have the previous name servers for the subdomain in their cache\.

1. After the registrar's TTL settings for the domain expire \(see Step 2\), delete the following resource record sets from the zone file for the parent domain:

   + The resource record sets that you added to Amazon Route 53 as described in [Creating Resource Record Sets](#AddMigratedSubdomainRecords)\.

   + Your DNS service's NS records\. When you are finished deleting NS records, the only NS records in the zone file will be the ones that you created in Step 4\.