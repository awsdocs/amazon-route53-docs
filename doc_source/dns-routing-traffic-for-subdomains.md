# Routing traffic for subdomains<a name="dns-routing-traffic-for-subdomains"></a>

When you want to route traffic to your resources for a subdomain, such as acme\.example\.com or zenith\.example\.com, you have two options:

**Create records in the hosted zone for the domain**  
Typically, to route traffic for a subdomain, you create a record in the hosted zone that has the same name as the domain\. For example, to route internet traffic for acme\.example\.com to a web server in your data center, you create a record named acme\.example\.com in the example\.com hosted zone\. For more information, see the topic [Working with records](rrsets-working-with.md) and its subtopics\.

**Create a hosted zone for the subdomain, and create records in the new hosted zone**  
You can also create a hosted zone for the subdomain\. Using a separate hosted zone to route internet traffic for a subdomain is sometimes known as "delegating responsibility for a subdomain to a hosted zone" or "delegating a subdomain to other name servers" or some similar combination of terms\. Here's an overview of how it works:  

1. You create a hosted zone that has the same name as the subdomain that you want to route traffic for, such as acme\.example\.com\.

1. You create records in the new hosted zone that define how you want to route traffic for the subdomain \(acme\.example\.com\) and its subdomains, such as backend\.acme\.example\.com\. 

1. You get the name servers that Route 53 assigned to the new hosted zone when you created it\.

1. You create a new NS record in the hosted zone for the domain \(example\.com\), and you specify the four name servers that you got in step 3\.
When you use a separate hosted zone to route traffic for a subdomain, you can use IAM permissions to restrict access to the hosted zone for the subdomain\. \(You can't use IAM to control access to individual records\.\) If you have multiple subdomains that are managed by different groups, creating a hosted zone for each subdomain can significantly reduce the number of people who must have access to records in the hosted zone for the domain\.  
Using a separate hosted zone for a subdomain also allows you to use different DNS services for the domain and the subdomain\. For more information, see [Using Amazon Route 53 as the DNS service for subdomains without migrating the parent domain](creating-migrating.md)\.  
There's a small performance impact to this configuration for the first DNS query from each DNS resolver\. The resolver must get information from the hosted zone for the root domain and then get information from the hosted zone for the subdomain\. After the first DNS query for a subdomain, the resolver caches the information and doesn't need to get it again until the TTL expires and another client requests the subdomain from that resolver\. For more information, see [TTL \(time to live\)](resource-record-sets-values-basic.md#rrsets-values-basic-ttl) in the section [Values that you specify when you create or edit Amazon Route 53 records](resource-record-sets-values.md)\.

**Topics**
+ [Creating another hosted zone to route traffic for a subdomain](#dns-routing-traffic-for-subdomains-new-hosted-zone)
+ [Routing traffic for additional levels of subdomains](#dns-routing-traffic-for-sub-subdomains)

## Creating another hosted zone to route traffic for a subdomain<a name="dns-routing-traffic-for-subdomains-new-hosted-zone"></a>

One way to route traffic for a subdomain is to create a hosted zone for the subdomain, and then create records for the subdomain in the new hosted zone\. \(The more common option is to create records for the subdomain in the hosted zone for the domain\.\)

Here's an overview of the process:

1. Create a hosted zone for the subdomain\. For more information, see [Creating a new hosted zone for a subdomain](#dns-routing-traffic-for-subdomains-creating-hosted-zone)\. 

1. Add records to the hosted zone for the subdomain\. If the hosted zone for the domain contains any records that belong in the hosted zone for the subdomain, duplicate those records in the hosted zone for the subdomain\. For more information, see [Creating records in the hosted zone for the subdomain](#dns-routing-traffic-for-subdomains-creating-records) 

1. Create an NS record for the subdomain in the hosted zone for the domain, which delegates responsibility for the subdomain to the name servers in the new hosted zone\. If the hosted zone for the domain contains any records that belong in the hosted zone for the subdomain, delete the records from the hosted zone for the domain\. \(You created copies in the hosted zone for the subdomain in step 2\.\) For more information, see [Updating the hosted zone for the domain](#dns-routing-traffic-for-subdomains-delegating-responsibility)\.

### Creating a new hosted zone for a subdomain<a name="dns-routing-traffic-for-subdomains-creating-hosted-zone"></a>

To create a hosted zone for a subdomain using the Route 53 console, perform the following procedure\.

**To create a hosted zone for a subdomain \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get Started Now** under **DNS Management**\. 

   If you're already using Route 53, choose **Hosted zones** in the navigation pane\. 

1. Choose **Create Hosted Zone**\.

1. In the right pane, enter the name of the subdomain, such as acme\.example\.com\. You can also optionally enter a comment\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

1. For **Type**, accept the default value of **Public Hosted Zone**\.

1. At the bottom of the right pane, choose **Create**\.

### Creating records in the hosted zone for the subdomain<a name="dns-routing-traffic-for-subdomains-creating-records"></a>

To define how you want Route 53 to route traffic for the subdomain \(acme\.example\.com\) and its subdomains \(backend\.acme\.example\.com\), you create records in the hosted zone for the subdomain\.

Note the following about creating records in the hosted zone for the subdomain:
+ Don't create additional name server \(NS\) or start of authority \(SOA\) records in the hosted zone for the subdomain, and don't delete the existing NS and SOA records\.
+ Create all records for the subdomain in the hosted zone for the subdomain\. For example, if you have hosted zones for example\.com and for acme\.example\.com domain, create all records for the acme\.example\.com subdomain in the acme\.example\.com hosted zone\. This includes records such as backend\.acme\.example\.com and beta\.backend\.acme\.example\.com\.
+ If the hosted zone for the domain \(example\.com\) already contains records that belong in the hosted zone for the subdomain \(acme\.example\.com\), duplicate those records in the hosted zone for the subdomain\. In the last step of the process, you delete the duplicate records from the hosted zone for the domain later\.
**Important**  
If you have some records for the subdomain in both the hosted zone for the domain and the hosted zone for the subdomain, DNS behavior will be inconsistent\. Behavior will depend on which name servers a DNS resolver has cached, the name servers for the domain hosted zone \(example\.com\) or the name servers for the subdomain hosted zone \(acme\.example\.com\)\. In some cases, Route 53 will return NXDOMAIN \(non\-existent domain\) when the record exists, but not in the hosted zone that DNS resolvers are submitting the query to\.

For more information, see [Working with records](rrsets-working-with.md)\.

### Updating the hosted zone for the domain<a name="dns-routing-traffic-for-subdomains-delegating-responsibility"></a>

When you create a hosted zone, Route 53 automatically assigns four name servers to the zone\. The NS record for a hosted zone identifies the name servers that respond to DNS queries for the domain or subdomain\. To start using the records in the hosted zone for the subdomain to route internet traffic, you create a new NS record in the hosted zone for the domain \(example\.com\), and give it the name of the subdomain \(acme\.example\.com\)\. For the value of the NS record, you specify the names of the name servers from the hosted zone for the subdomain\. 

Here's what happens when Route 53 receives a DNS query from a DNS resolver for the subdomain acme\.example\.com or one of its subdomains:

1. Route 53 looks in the hosted zone for the domain \(example\.com\) and finds the NS record for the subdomain \(acme\.example\.com\)\.

1. Route 53 gets the name servers from the acme\.example\.com NS record in the hosted zone for the domain, example\.com, and returns those name servers to the DNS resolver\. 

1. The resolver resubmits the query for acme\.example\.com to the name servers for the acme\.example\.com hosted zone\.

1. Route 53 responds to the query using a record in the acme\.example\.com hosted zone\.

To configure Route 53 to route traffic for the subdomain using the hosted zone for the subdomain and to delete any duplicate records from the hosted zone for the domain, perform the following procedure:

**To configure Route 53 to use the hosted zone for the subdomain \(console\)**

1. In the Route 53 console, get the name servers for the hosted zone for the subdomain:

   1. In the navigation pane, choose **Hosted zones**\. 

   1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone for the subdomain\.

   1. In the right pane, copy the names of the four servers listed for **Name Servers**\.

1. Choose the name of the hosted zone for the domain \(example\.com\), not for the subdomain\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the name of the subdomain\.  
**Type**  
Choose **NS – Name server**\.  
**TTL \(Seconds\)**  
Change to a more common value for an NS record, such as 172800 seconds\.  
**Value**  
Paste the names of the name servers that you copied in step 1\.  
**Routing Policy**  
Accept the default value of **Simple**\.

1. Choose **Create**\.

1. If the hosted zone for the domain contains any records that you recreated in the hosted zone for the subdomain, delete those records from the hosted zone for the domain\. For more information, see [Deleting records](resource-record-sets-deleting.md)\.

   When you're finished, all records for the subdomain should be in the hosted zone for the subdomain\.

## Routing traffic for additional levels of subdomains<a name="dns-routing-traffic-for-sub-subdomains"></a>

You route traffic to a subdomain of a subdomain, such as backend\.acme\.example\.com, the same way that you route traffic to a subdomain, such as acme\.example\.com\. Either you create records in the hosted zone for the domain, or you create a hosted zone for the lower\-level subdomain, and then you create records in that new hosted zone\.

If you choose to create a separate hosted zone for the lower\-level subdomain, create the NS record for the lower\-level subdomain in the hosted zone for the subdomain that is one level closer to the domain name\. This helps to ensure that traffic is correctly routed to your resources\. For example, suppose you want to route traffic for the following subdomains:
+ subdomain1\.example\.com
+ subdomain2\.subdomain1\.example\.com

To use another hosted zone to route traffic for subdomain2\.subdomain1\.example\.com, you do the following:

1. Create a hosted zone named subdomain2\.subdomain1\.example\.com\. 

1. Create records in the subdomain2\.subdomain1\.example\.com hosted zone\. For more information, see [Creating records in the hosted zone for the subdomain](#dns-routing-traffic-for-subdomains-creating-records)\.

1. Copy the names of the name servers for the subdomain2\.subdomain1\.example\.com hosted zone\. 

1. In the subdomain1\.example\.com hosted zone, create an NS record named subdomain2\.subdomain1\.example\.com, and paste in the names of the name servers for the subdomain2\.subdomain1\.example\.com hosted zone\. 

   In addition, delete any duplicate records from the subdomain1\.example\.com\. For more information, see [Updating the hosted zone for the domain](#dns-routing-traffic-for-subdomains-delegating-responsibility)\. 

   After you create this NS record, Route 53 starts to use the subdomain2\.subdomain1\.example\.com hosted zone to route traffic for the subdomain2\.subdomain1\.example\.com subdomain\.