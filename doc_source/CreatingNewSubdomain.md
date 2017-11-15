# Creating a Subdomain That Uses Amazon Route 53 as the DNS Service without Migrating the Parent Domain<a name="CreatingNewSubdomain"></a>

You can create a subdomain that uses Amazon Route 53 as the DNS service without migrating the parent domain from another DNS service\.

The process has four basic steps:

1. Create an Amazon Route 53 hosted zone for the subdomain\.

1. Add resource record sets for the new subdomain to your Amazon Route 53 hosted zone\.

1. *API only:* Confirm that your changes have propagated to all Amazon Route 53 DNS servers\.
**Note**  
Currently, the only way to verify that changes have propagated is to use the [GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API action\. Changes generally propagate to all Amazon Route 53 name servers within 60 seconds\.

1. Update the DNS service for the parent domain by adding name server records for the subdomain\.

## Creating a Hosted Zone for the New Subdomain<a name="CreateZoneNewSubdomain"></a>

When you want to use Amazon Route 53 as the DNS service for a new subdomain without migrating the parent domain, you start by creating a hosted zone for the subdomain\. Amazon Route 53 stores information about your subdomain in the hosted zone\.

When you create a hosted zone, Amazon Route 53 automatically creates four name server \(NS\) records and a start of authority \(SOA\) record for the zone\. The NS records identify the name servers that you give to your registrar or your DNS service so that queries are routed to Amazon Route 53 name servers\. For more information about NS and SOA records, see [NS and SOA Resource Record Sets that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)\.

To create a hosted zone using the Amazon Route 53 console, perform the following procedure\. To create a hosted zone using the Amazon Route 53 API, use the `CreateHostedZone` action\. For more information, see [CreateHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html) in the *Amazon Route 53 API Reference*\.

**To create a hosted zone using the Amazon Route 53 console**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Amazon Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Amazon Route 53, choose **Hosted Zones** in the **navigation** pane\.

1. In the right pane, enter the name of the subdomain, such as **apex\.example\.com**\. You can also enter an optional comment\. For more information about a field, see the tool tip for the field\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

1. Below the right pane, choose **Create Hosted Zone**\.

## Creating Resource Record Sets<a name="AddNewSubdomainRecords"></a>

You can create resource record sets using either the Amazon Route 53 console or the Amazon Route 53 API\. The resource record sets that you create in Amazon Route 53 will become the resource record sets that DNS uses after you delegate responsibility for the subdomain to Amazon Route 53, as explained in [Updating Your DNS Service with Name Server Records for the Subdomain](#UpdateDNSParentDomain), later in the process\.

**Important**  
Do not create additional name server \(NS\) or start of authority \(SOA\) records in the Amazon Route 53 hosted zone, and do not delete the existing NS and SOA records\. 

To create resource record sets using the Amazon Route 53 console, see [Working with Resource Record Sets](rrsets-working-with.md)\. To create resource record sets using the Amazon Route 53 API, use `ChangeResourceRecordSets`\. For more information, see [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *[Amazon Route 53 API Reference](http://docs.aws.amazon.com/Route53/latest/APIReference/)*\.

## Checking the Status of Your Changes \(API Only\)<a name="CheckStatusNewSubdomain"></a>

Creating a new hosted zone and changing resource record sets take time to propagate to the Amazon Route 53 DNS servers\. If you used [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) to create your resource record sets, you can use the `GetChange` action to determine whether your changes have propagated\. \(`ChangeResourceRecordSets` returns a value for `ChangeId`, which you can include in a subsequent `GetChange` request\. `ChangeId` is not available if you created the resource record sets by using the console\.\) For more information, see [GET GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) in the *Amazon Route 53 API Reference*\.

**Note**  
Changes generally propagate to all Amazon Route 53 name servers within 60 seconds\.

## Updating Your DNS Service with Name Server Records for the Subdomain<a name="UpdateDNSParentDomain"></a>

After your changes to Amazon Route 53 resource record sets have propagated \(see [Checking the Status of Your Changes \(API Only\)](#CheckStatusNewSubdomain)\), update the DNS service for the parent domain by adding NS records for the subdomain\. This is known as delegating responsibility for the subdomain to Amazon Route 53\. For example, if the parent domain example\.com is hosted with another DNS service and you created the subdomain test\.example\.com in Amazon Route 53, you must update the DNS service for example\.com with new NS records for test\.example\.com\.

Perform the following procedure\.

1. Using the method provided by your DNS service, back up the zone file for the parent domain\.

1. In the Amazon Route 53 console, get the name servers for your Amazon Route 53 hosted zone:

   1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, click **Hosted Zones**\.

   1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.

   1. In the right pane, make note of the four servers listed for **Name Servers**\.

   Alternatively, you can use the `GetHostedZone` action\. For more information, see [GetHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html) in the *Amazon Route 53 API Reference*\.

1. Using the method provided by the DNS service of the parent domain, add NS records for the subdomain to the zone file for the parent domain\. In these NS records, specify the four Amazon Route 53 name servers that are associated with the hosted zone that you created in Step 1\.

**Important**  
Do not add a start of authority \(SOA\) record to the zone file for the parent domain\. Because the subdomain will use Amazon Route 53, the DNS service for the parent domain is not the authority for the subdomain\.   
If your DNS service automatically added an SOA record for the subdomain, delete the record for the subdomain\. However, do not delete the SOA record for the parent domain\.