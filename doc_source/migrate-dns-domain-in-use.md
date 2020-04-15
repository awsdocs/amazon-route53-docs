# Making Route 53 the DNS service for a domain that's in use<a name="migrate-dns-domain-in-use"></a>

If you want to migrate DNS service to Amazon Route 53 for a domain that is currently getting traffic—for example, if your users are using the domain name to browse to a website or access a web application—perform the procedures in this section\.

**Topics**
+ [Step 1: Get your current DNS configuration from the current DNS service provider \(optional but recommended\)](#migrate-dns-get-zone-file)
+ [Step 2: Create a hosted zone](#migrate-dns-create-hosted-zone)
+ [Step 3: Create records](#migrate-dns-create-records)
+ [Step 4: Lower TTL settings](#migrate-dns-lower-ttl)
+ [Step 5: Wait for the old TTL to expire](#migrate-dns-wait-for-ttl)
+ [Step 6: Update the NS record with your current DNS service provider to use Route 53 name servers](#migrate-dns-change-name-servers-with-provider)
+ [Step 7: Monitor traffic for the domain](#migrate-dns-monitor-traffic)
+ [Step 8: Update the domain registration to use Amazon Route 53 name servers](#migrate-dns-update-domain)
+ [Step 9: Change the TTL for the NS record back to a higher value](#migrate-dns-change-ttl-back)
+ [Step 10: Transfer domain registration to Amazon Route 53](#migrate-dns-transfer-domain-registration)

## Step 1: Get your current DNS configuration from the current DNS service provider \(optional but recommended\)<a name="migrate-dns-get-zone-file"></a>

When you migrate DNS service from another provider to Route 53, you reproduce your current DNS configuration in Route 53\. In Route 53, you create a hosted zone that has the same name as your domain, and you create records in the hosted zone\. Each record indicates how you want to route traffic for a specified domain name or subdomain name\. For example, when someone enters your domain name in a web browser, do you want traffic to be routed to a web server in your data center, to an Amazon EC2 instance, to a CloudFront distribution, or to some other location?

The process that you use depends on the complexity of your current DNS configuration:
+ **If your current DNS configuration is simple** – If you're routing internet traffic for just a few subdomains to a small number of resources, such as web servers or Amazon S3 buckets, then you can manually create a few records in the Route 53 console\.
+ **If your current DNS configuration is more complex, and you just want to reproduce your current configuration** – You can simplify the migration if you can get a zone file from the current DNS service provider, and import the zone file into Route 53\. \(Not all DNS service providers offer zone files\.\) When you import a zone file, Route 53 automatically reproduces the existing configuration by creating the corresponding records in your hosted zone\.

  Try asking customer support with your current DNS service provider how to get a *zone file* or a *records list*\. For information about the required format of the zone file, see [Creating records by importing a zone file](resource-record-sets-creating-import.md)\.
+ **If your current DNS configuration is more complex, and you're interested in Route 53 routing features** – Review the following documentation to see whether you want to use Route 53 features that aren't available from other DNS service providers\. If so, you can either create records manually, or you can import a zone file and then create or update records later:
  + [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md) explains the advantages of Route 53 alias records, which route traffic to some AWS resources, such as CloudFront distributions and Amazon S3 buckets, for no charge\.
  + [Choosing a routing policy](routing-policy.md) explains the Route 53 routing options, for example, routing based on the location of your users, routing based on the latency between your users and your resources, routing based on whether your resources are healthy, and routing to resources based on weights that you specify\.
**Note**  
You can also import a zone file and later change your configuration to take advantage of alias records and complex routing policies\.

If you can't get a zone file or if you want to manually create records in Route 53, the records that you're likely to migrate include the following:
+ **A \(Address\) records** – associate a domain name or subdomain name with the IPv4 address \(for example, 192\.0\.2\.3\) of the corresponding resource
+ **AAAA \(Address\) records** – associate a domain name or subdomain name with the IPv6 address \(for example, 2001:0db8:85a3:0000:0000:abcd:0001:2345\) of the corresponding resource
+ **Mail server \(MX\) records** – route traffic to mail servers
+ **CNAME records** – reroute traffic for one domain name \(example\.net\) to another domain name \(example\.com\)
+ **Records for other supported DNS record types** – For a list of supported record types, see [Supported DNS record types](ResourceRecordTypes.md)\.

## Step 2: Create a hosted zone<a name="migrate-dns-create-hosted-zone"></a>

To tell Amazon Route 53 how you want to route traffic for your domain, you create a hosted zone that has the same name as your domain, and then you create records in the hosted zone\. 

**Important**  
You can create a hosted zone only for a domain that you have permission to administer\. Typically, this means that you own the domain, but you might also be developing an application for the domain registrant\.

When you create a hosted zone, Route 53 automatically creates a name server \(NS\) record and a start of authority \(SOA\) record for the zone\. The NS record identifies the four name servers that Route 53 associated with your hosted zone\. To make Route 53 the DNS service for your domain, you update the registration for the domain to use these four name servers\. 

**Important**  
Don't create additional name server \(NS\) or start of authority \(SOA\) records, and don't delete the existing NS and SOA records\. <a name="migrate-dns-create-hosted-zone-procedure"></a>

**To create a hosted zone**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Route 53, choose **Hosted Zones** in the navigation pane\.

1. Choose **Create Hosted Zone**\.

1. In the **Create Hosted Zone** pane, enter a domain name and, optionally, a comment\. For more information about a setting, pause the mouse pointer over its label to see a tool tip\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

1. For **Type**, accept the default value of **Public Hosted Zone**\.

1. Choose **Create**\.

## Step 3: Create records<a name="migrate-dns-create-records"></a>

After you create a hosted zone, you create records in the hosted zone that define where you want to route traffic for a domain \(example\.com\) or subdomain \(www\.example\.com\)\. For example, if you want to route traffic for example\.com and www\.example\.com to a web server on an Amazon EC2 instance, you create two records, one named example\.com and the other named www\.example\.com\. In each record, you specify the IP address for your EC2 instance\.

You can create records in a variety of ways:

**Import a zone file**  
This is the easiest method if you got a zone file from your current DNS service in [Step 1: Get your current DNS configuration from the current DNS service provider \(optional but recommended\)](#migrate-dns-get-zone-file)\. Amazon Route 53 can't predict when to create alias records or to use special routing types such as weighted or failover\. As a result, if you import a zone file, Route 53 creates standard DNS records using the simple routing policy\.  
For more information, see [Creating records by importing a zone file](resource-record-sets-creating-import.md)\.

**Create records individually in the console**  
If you didn't get a zone file and you just want to create a few records with a routing policy of Simple to get started, you can create the records in the Route 53 console\. You can create both alias and non\-alias records\.  
For more information, see the following topics:  
+ [Choosing a routing policy](routing-policy.md)
+ [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)
+ [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)

**Create records programmatically**  
You can create records by using one of the AWS SDKs, the AWS CLI, or AWS Tools for Windows PowerShell\. For more information, see [AWS Documentation](https://docs.aws.amazon.com/)\.  
If you're using a programming language that AWS doesn't provide an SDK for, you can also use the Route 53 API\. For more information, see the [Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/)\.

## Step 4: Lower TTL settings<a name="migrate-dns-lower-ttl"></a>

The TTL \(time to live\) setting for a record specifies how long you want DNS resolvers to cache the record and use the cached information\. When the TTL expires, a resolver sends another query to the DNS service provider for a domain to get the latest information\.

The typical TTL setting for the NS record is 172800 seconds, or two days\. The NS record lists the name servers that the Domain Name System \(DNS\) can use to get information about how to route traffic for your domain\. Lowering the TTL for the NS record, both with your current DNS service provider and with Amazon Route 53, reduces downtime for your domain if you discover a problem while you're migrating DNS to Route 53\. If you don't lower the TTL, your domain could be unavailable on the internet for up to two days if something goes wrong\.

We recommend that you change the TTL on the following NS records:
+ On the NS record in the hosted zone for the current DNS service provider\. \(Your current provider might use different terminology\.\)
+ On the NS record in the hosted zone that you created in [Step 2: Create a hosted zone](#migrate-dns-create-hosted-zone)\.<a name="migrate-dns-lower-ttl-current-provider-procedure"></a>

**To lower the TTL setting on the NS record with the current DNS service provider**
+ Use the method provided by the current DNS service provider for the domain to change the TTL for the NS record in the hosted zone for your domain\.<a name="migrate-dns-lower-ttl-route-53-procedure"></a>

**To lower the TTL setting on the NS record in a Route 53 hosted zone**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Choose **Hosted Zones** in the navigation pane\.

1. Choose the name of the hosted zone\.

1. Choose the NS record\.

1. Change the value of **TTL \(Seconds\)**\. We recommend that you specify a value between 60 seconds and 900 seconds \(15 minutes\)\.

1. Choose **Save Record Set**\.

## Step 5: Wait for the old TTL to expire<a name="migrate-dns-wait-for-ttl"></a>

If your domain is in use—for example, if your users are using the domain name to browse to a website or access a web application—then DNS resolvers have cached the names of the name servers that were provided by your current DNS service provider\. A DNS resolver that cached that information a few minutes ago will save it for almost two more days\.

To ensure that migrating DNS service to Route 53 happens all at one time, wait for two days after you lowered the TTL\. After the two\-day TTL expires and resolvers request the name servers for your domain, the resolvers will get the current name servers and will also get the new TTL that you specified in [Step 4: Lower TTL settings](#migrate-dns-lower-ttl)\.

## Step 6: Update the NS record with your current DNS service provider to use Route 53 name servers<a name="migrate-dns-change-name-servers-with-provider"></a>

To begin using Amazon Route 53 as the DNS service for a domain, use the method provided by the current DNS service provider to replace the current name servers in the NS record with Route 53 name servers\.

**Note**  
When you update the NS record with the current DNS service provider to use Route 53 name servers, you're updating the DNS configuration for the domain\. \(This is comparable to updating the NS record in the Route 53 hosted zone for a domain except that you're updating the setting with the DNS service that you're migrating away from\.\)   
In [Step 8: Update the domain registration to use Amazon Route 53 name servers](#migrate-dns-update-domain), you update the domain registration to use the same four name servers\. The domain can be registered with Route 53 or with another domain registrar\.<a name="migrate-dns-change-name-servers-with-provider-procedure"></a>

**To update the NS record with your current DNS service provider to use Route 53 name servers**

1. In the Route 53 console, get the name servers for your hosted zone:

   1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, choose **Hosted zones**\.

   1. On the **Hosted zones** page, choose the radio button \(not the name\) for the applicable hosted zone\.

   1. Make note of the four names listed for **Name Servers**\.

1. Use the method that is provided by the current DNS service for the domain to update the NS record for the hosted zone\. The process depends on whether the current DNS service lets you delete name servers:

   **If you can delete name servers**
   + Make note of the names of the current name servers in the NS record for the hosted zone\. If you need to revert to the current DNS configuration, these are the servers that you'll specify\.
   + Delete the current name servers from the NS record\. 
   + Update the NS record with the names of all four of the Route 53 name servers that you got in step 1 of this procedure\.
**Note**  
When you're finished, the only name servers in the NS record will be the four Route 53 name servers\.

   **If you cannot delete name servers**
   + Choose the option to use custom name servers\.
   + Add all four Route 53 name servers that you got in step 1 of this procedure\. 

## Step 7: Monitor traffic for the domain<a name="migrate-dns-monitor-traffic"></a>

Monitor traffic for the domain, including website or application traffic, and email:
+ **If the traffic slows or stops** – Use the method provided by the previous DNS service to change the name servers for the domain back to the previous name servers\. These are the name servers that you made note of in step 2 of [To update the NS record with your current DNS service provider to use Route 53 name servers](#migrate-dns-change-name-servers-with-provider-procedure)\. Then determine what went wrong\.
+ **If the traffic is unaffected** – Continue to [Step 8: Update the domain registration to use Amazon Route 53 name servers](#migrate-dns-update-domain)\.

## Step 8: Update the domain registration to use Amazon Route 53 name servers<a name="migrate-dns-update-domain"></a>

When you're confident that migrating DNS service to Route 53 was successful, you can change the DNS service for your domain to Amazon Route 53\. Perform the following procedure to update settings with the domain registrar\.<a name="migrate-dns-update-domain-procedure"></a>

**To update the name servers for the domain**

1. In the Route 53 console, get the name servers for your Route 53 hosted zone:

   1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, choose **Hosted zones**\.

   1. On the **Hosted zones** page, choose the radio button \(not the name\) for the applicable hosted zone\.

   1. Make note of the four names listed for **Name Servers**\.

1. Use the method provided by the registrar for the domain to change the name servers for the domain to use the four Route 53 name servers that you got in step 1 of this procedure\.

   If the domain is registered with Route 53, see [Adding or changing name servers and glue records for a domain](domain-name-servers-glue-records.md)\.

## Step 9: Change the TTL for the NS record back to a higher value<a name="migrate-dns-change-ttl-back"></a>

In the Amazon Route 53 hosted zone for the domain, change the TTL for the NS record to a more typical value, for example, 172800 seconds \(two days\)\. This improves latency for your users because they don't have to wait as often for DNS resolvers to send a query for the name servers for your domain\.<a name="migrate-dns-change-ttl-back-procedure"></a>

**To change the TTL for the NS record in the Route 53 hosted zone**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Choose **Hosted Zones** in the navigation pane\.

1. Choose the name of the hosted zone\.

1. In the list of records for the hosted zone, choose the NS record\.

1. Change **TTL \(Seconds\)** to the number of seconds that you want DNS resolvers to cache the names of the name servers for your domain\. We recommend a value of 172800 seconds\.

1. Choose **Save Record Set**\.

## Step 10: Transfer domain registration to Amazon Route 53<a name="migrate-dns-transfer-domain-registration"></a>

Now that you've transferred DNS service for a domain to Amazon Route 53, you can optionally transfer registration for the domain to Route 53\. For more information, see [Transferring registration for a domain to Amazon Route 53](domain-transfer-to-route-53.md)\.