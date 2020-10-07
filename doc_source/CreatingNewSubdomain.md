# Creating a subdomain that uses Amazon Route 53 as the DNS service without migrating the parent domain<a name="CreatingNewSubdomain"></a>

You can create a subdomain that uses Amazon Route 53 as the DNS service without migrating the parent domain from another DNS service\.

The process has the following basic steps:

1. [Figure out](#decide-procedure-create-subdomain) whether you should even be using this procedure\.

1. [Create a Route 53 hosted zone for the subdomain](#CreateZoneNewSubdomain)\.

1. [Add records](#AddNewSubdomainRecords) for the new subdomain to your Route 53 hosted zone\.

1. *API only:* [Confirm that your changes have propagated](#CheckStatusNewSubdomain) to all Route 53 DNS servers\.
**Note**  
Currently, the only way to verify that changes have propagated is to use the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API action\. Changes generally propagate to all Route 53 name servers within 60 seconds\.

1. [Update the DNS service for the parent domain by adding name server records for the subdomain](#UpdateDNSParentDomain)\.

## Deciding which procedures to use for creating a subdomain<a name="decide-procedure-create-subdomain"></a>

The procedures in this topic explain how to perform an uncommon operation\. If you're already using Route 53 as the DNS service for your domain and you just want to route traffic for a subdomain, such as www\.example\.com, to your resources, such as a web server running on an EC2 instance, see [Routing traffic for subdomains](dns-routing-traffic-for-subdomains.md)\.

Use this procedure *only* if you're using another DNS service for a domain, such as example\.com, and you want to start using Route 53 as the DNS service for a new subdomain of that domain, such as www\.example\.com\.

## Creating a hosted zone for the new subdomain<a name="CreateZoneNewSubdomain"></a>

When you want to use Amazon Route 53 as the DNS service for a new subdomain without migrating the parent domain, you start by creating a hosted zone for the subdomain\. Route 53 stores information about your subdomain in the hosted zone\.

For information about how to create a hosted zone using the Route 53 console, see [Creating a public hosted zone](CreatingHostedZone.md)\.

## Creating records<a name="AddNewSubdomainRecords"></a>

You can create records using either the Amazon Route 53 console or the Route 53 API\. The records that you create in Route 53 will become the records that DNS uses after you delegate responsibility for the subdomain to Route 53, as explained in [Updating your DNS service with name server records for the subdomain](#UpdateDNSParentDomain), later in the process\.

**Important**  
Do not create additional name server \(NS\) or start of authority \(SOA\) records in the Route 53 hosted zone, and do not delete the existing NS and SOA records\. 

To create records using the Route 53 console, see [Working with records](rrsets-working-with.md)\. To create records using the Route 53 API, use `ChangeResourceRecordSets`\. For more information, see [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *[Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/)*\.

## Checking the status of your changes \(API only\)<a name="CheckStatusNewSubdomain"></a>

Creating a new hosted zone and changing records take time to propagate to the Route 53 DNS servers\. If you used [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) to create your records, you can use the `GetChange` action to determine whether your changes have propagated\. \(`ChangeResourceRecordSets` returns a value for `ChangeId`, which you can include in a subsequent `GetChange` request\. `ChangeId` is not available if you created the records by using the console\.\) For more information, see [GET GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) in the *Amazon Route 53 API Reference*\.

**Note**  
Changes generally propagate to all Route 53 name servers within 60 seconds\.

## Updating your DNS service with name server records for the subdomain<a name="UpdateDNSParentDomain"></a>

After your changes to Amazon Route 53 records have propagated \(see [Checking the status of your changes \(API only\)](#CheckStatusNewSubdomain)\), update the DNS service for the parent domain by adding NS records for the subdomain\. This is known as delegating responsibility for the subdomain to Route 53\. For example, if the parent domain example\.com is hosted with another DNS service and you created the subdomain test\.example\.com in Route 53, you must update the DNS service for example\.com with new NS records for test\.example\.com\.

Perform the following procedure\.

1. Using the method provided by your DNS service, back up the zone file for the parent domain\.

1. In the Route 53 console, get the name servers for your Route 53 hosted zone:

   1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, click **Hosted Zones**\.

   1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.

   1. In the right pane, make note of the four servers listed for **Name Servers**\.

   Alternatively, you can use the `GetHostedZone` action\. For more information, see [GetHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html) in the *Amazon Route 53 API Reference*\.

1. Using the method provided by the DNS service of the parent domain, add NS records for the subdomain to the zone file for the parent domain\. In these NS records, specify the four Route 53 name servers that are associated with the hosted zone that you created in Step 1\.

**Important**  
Do not add a start of authority \(SOA\) record to the zone file for the parent domain\. Because the subdomain will use Route 53, the DNS service for the parent domain is not the authority for the subdomain\.   
If your DNS service automatically added an SOA record for the subdomain, delete the record for the subdomain\. However, do not delete the SOA record for the parent domain\.