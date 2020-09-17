# Configuring white\-label name servers<a name="white-label-name-servers"></a>

Each Amazon Route 53 hosted zone is associated with four name servers, known collectively as a delegation set\. By default, the name servers have names like ns\-2048\.awsdns\-64\.com\. If you want the domain name of your name servers to be the same as the domain name of your hosted zone, for example, ns1\.example\.com, you can configure white\-label name servers, also known as vanity name servers or private name servers\.

The following steps explain how to configure one set of four white\-label name servers that you can reuse for multiple domains\. For example, suppose you own the domains example\.com, example\.org, and example\.net\. With these steps, you can configure white\-label name servers for example\.com and reuse them for example\.org and example\.net\.

**Topics**
+ [Step 1: Create a Route 53 reusable delegation set](#white-label-name-servers-create-reusable-delegation-set)
+ [Step 2: Create or recreate Amazon Route 53 hosted zones, and change the TTL for NS and SOA records](#white-label-name-servers-create-hosted-zones)
+ [Step 3: Recreate records for your hosted zones](#white-label-name-servers-create-resource-record-sets)
+ [Step 4: Get IP addresses](#white-label-name-servers-get-ip-addresses)
+ [Step 5: Create records for white\-label name servers](#white-label-name-servers-create-white-label-resource-record-sets)
+ [Step 6: Update NS and SOA records](#white-label-name-servers-update-ns-soa-records)
+ [Step 7: Create glue records and change the registrar's name servers](#white-label-name-servers-create-glue-records)
+ [Step 8: Monitor traffic for the website or application](#white-label-name-servers-monitor-traffic)
+ [Step 9: Change TTLs back to their original values](#white-label-name-servers-change-ttls-back)
+ [Step 10: \(Optional\) contact recursive DNS services](#white-label-name-servers-contact-recursive-dns-services)

## Step 1: Create a Route 53 reusable delegation set<a name="white-label-name-servers-create-reusable-delegation-set"></a>

White\-label name servers are associated with a Route 53 reusable delegation set\. You can use white\-label name servers for a hosted zone only if the hosted zone and the reusable delegation set were created by the same AWS account\.

To create a reusable delegation set, you can use the Route 53 API, the AWS CLI, or one of the AWS SDKs\. For more information, see the following documentation: 
+ **Route 53 API** – See [CreateReusableDelegationSet](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateReusableDelegationSet.html) in the *Amazon Route 53 API Reference* 
+ **AWS CLI** – See [create\-reusable\-delegation\-set](https://docs.aws.amazon.com/cli/latest/reference/route53/create-reusable-delegation-set.html) in the *AWS CLI Command Reference*
+ **AWS SDKs** See the applicable SDK documentation on the [AWS Documentation](https://docs.aws.amazon.com/) page

## Step 2: Create or recreate Amazon Route 53 hosted zones, and change the TTL for NS and SOA records<a name="white-label-name-servers-create-hosted-zones"></a>

Create or recreate Amazon Route 53 hosted zones:
+ **If you aren't currently using Route 53 as the DNS service for the domains for which you want to use white\-label name servers** – Create the hosted zones and specify the reusable delegation set that you created in the previous step with each hosted zone\. For more information, see [CreateHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html) in the *Amazon Route 53 API Reference*\. 
+ **If you are using Route 53 as the DNS service for the domains for which you want to use white\-label name servers** – You must recreate the hosted zones for which you want to use white\-label name servers, and specify the reusable delegation set that you created in the previous step for each hosted zone\.
**Important**  
You cannot change the name servers that are associated with an existing hosted zone\. You can associate a reusable delegation set with a hosted zone only when you create the hosted zone\.

When you create the hosted zones and before you try to access the resources for the corresponding domains, change the following TTL values for each hosted zone:
+ Change the TTL for the NS record for the hosted zone to 60 seconds or less\. 
+ Change the minimum TTL for the SOA record for the hosted zone to 60 seconds or less\. This is the last value in the SOA record\.

If you accidentally give your registrar the wrong IP addresses for your white\-label name servers, your website will become unavailable and remain unavailable for the duration of the TTL after you correct the problem\. By setting a low TTL, you reduce the amount of time that your website is unavailable\.

For more information about creating hosted zones and specifying a reusable delegation set for the name servers for the hosted zones, see [CreateHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html) in the *Amazon Route 53 API Reference*\.

## Step 3: Recreate records for your hosted zones<a name="white-label-name-servers-create-resource-record-sets"></a>

Create records in the hosted zones that you created in Step 2:
+ **If you're migrating DNS service for your domains to Amazon Route 53** – You might be able to create records by importing information about your existing records\. For more information, see [Creating records by importing a zone file](resource-record-sets-creating-import.md)\.
+ **If you're replacing existing hosted zones so that you can use white\-label name servers** – In the new hosted zones, recreate the records that appear in your current hosted zones\. Route 53 doesn't provide a method of exporting records from a hosted zone, but some third\-party vendors do\. You can then use the Route 53 import feature to import non\-alias records for which the routing policy is simple\. There is no way to export and re\-import alias records or records for which the routing policy is anything other than simple\.

  For information about creating records by using the Route 53 API, see [CreateHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html) in the *Amazon Route 53 API Reference*\. For information about creating records by using the Route 53 console, see [Working with records](rrsets-working-with.md)\.

## Step 4: Get IP addresses<a name="white-label-name-servers-get-ip-addresses"></a>

Get the IPv4 and IPv6 addresses of the name servers in the reusable delegation set, and fill in the following table\. 


****  

| Name of a name server in your reusable delegation set \(example: Ns\-2048\.awsdns\-64\.com\) | IPv4 and IPv6 addresses                                             | Name that you want to assign to the white\-label name server \(example: ns1\.example\.com\) | 
| --- | --- | --- | 
|   | IPv4: IPv6:   |   | 
|   | IPv4: IPv6:   |   | 
|   | IPv4: IPv6:   |   | 
|   | IPv4: IPv6:   |   | 

For example, suppose the four name servers for your reusable delegation set are:
+ ns\-2048\.awsdns\-64\.com
+ ns\-2049\.awsdns\-65\.net
+ ns\-2050\.awsdns\-66\.org
+ ns\-2051\.awsdns\-67\.co\.uk

Here are the Linux and Windows commands that you'd run to get the IP addresses for the first of your four name servers:

**dig commands for Linux**

```
% dig A ns-2048.awsdns-64.com +short
192.0.2.117
```

```
% dig AAAA ns-2048.awsdns-64.com +short
2001:db8:85a3::8a2e:370:7334
```

**nslookup command for Windows**

```
c:\> nslookup ns-2048.awsdns-64.com
Non-authoritative answer:
Name:    ns-2048.awsdns-64.com
Addresses:  2001:db8:85a3::8a2e:370:7334
          192.0.2.117
```

## Step 5: Create records for white\-label name servers<a name="white-label-name-servers-create-white-label-resource-record-sets"></a>

In the hosted zone that has the same name \(such as example\.com\) as the domain name of the white\-label name servers \(such as ns1\.example\.com\), create eight records: 
+ One A record for each white\-label name server
+ One AAAA record for each white\-label name server

**Important**  
If you're using the same white\-label name servers for two or more hosted zones, do not perform this step for the other hosted zones\.

For each record, specify the following values\. Refer to the table that you filled in for the previous step:

**Name**  
The name that you want to assign to one of your white\-label name servers, for example, ns1\.example\.com\. For the prefix \(ns1 in this example\), you can use any value that is valid in a domain name\.

**Type**  
Specify **A** when you're creating records for the IPv4 addresses\.  
Specify **AAAA** when you're creating records for the IPv6 addresses\.

**Alias**  
Specify **No**\.

**TTL**  
This value is the amount of time that DNS resolvers cache the information in this record before forwarding another DNS query to Route 53\. We recommend that you specify an initial value of 60 seconds or less, so that you can recover quickly if you accidentally specify incorrect values in these records\.

**Value**  
The IPv4 or IPv6 address of one of the Route 53 name servers in your reusable delegation set\.  
If you specify the wrong IP addresses when you created records for your white\-label name servers, your website or web application will become unavailable on the internet when you perform subsequent steps\. Even if you correct the IP addresses immediately, your website or web application will remain unavailable for the duration of the TTL\.

**Routing Policy**  
Specify **Simple**\.

## Step 6: Update NS and SOA records<a name="white-label-name-servers-update-ns-soa-records"></a>

Update SOA and NS records in the hosted zones that you want to use white\-label name servers for\. Perform Step 6 through Step 8 for one hosted zone and the corresponding domain at a time, then repeat for another hosted zone and domain\.

**Important**  
Start with the Amazon Route 53 hosted zone that has the same domain name \(such as example\.com\) as the white\-label name servers \(such as ns1\.example\.com\)\.  
If you want to do either of the following, open a technical support case with AWS Support for help with the configuration:  
You want to use white\-label name servers \(ns1\.example\.com\) only for other domain names \(example\.net\), not for the domain name that you use for white\-label name servers \(example\.com\)\. If you don't contact AWS Support, you'll encounter the following error when you configure glue records in the next section: "One or more of the specified nameservers are not known to the domain registry\."
You currently use white\-label name servers \(ns1\.example\.com\) both for the domain name that you use for white\-label name servers \(example\.com\) and for other domains \(example\.net\)\. You want to stop using white\-label name servers for the example\.com domain, but continue to use them for other domains \(example\.net\)\. If you don't contact AWS Support, the other domains might become unavailable on the internet\.
To create a technical support case, see [AWS Support Center](https://console.aws.amazon.com/support/home)\.

1. Update the SOA record by replacing the name of the Route 53 name server with the name of one of your white\-label name servers

   **Example**

   Replace the name of the Route 53 name server:

   `ns-2048.awsdns-64.net. hostmaster.example.com. 1 7200 900 1209600 60`

   with the name of one of your white\-label name servers:

   `ns1.example.com. hostmaster.example.com. 1 7200 900 1209600 60`
**Note**  
You changed the last value, the time to live \(TTL\), in [Step 2: Create or recreate Amazon Route 53 hosted zones, and change the TTL for NS and SOA records](#white-label-name-servers-create-hosted-zones)\.

   For information about updating records by using the Route 53 console, see [Editing records](resource-record-sets-editing.md)\.

1. In the NS record, make note of the names of the current name servers for the domain, so you can revert to these name servers if necessary\.

1. Update the NS record\. Replace the name of the Route 53 name servers with the names of your four white\-label name servers, for example, `ns1.example.com`, `ns2.example.com`, `ns3.example.com`, and `ns4.example.com`\. 

## Step 7: Create glue records and change the registrar's name servers<a name="white-label-name-servers-create-glue-records"></a>

Use the method provided by the registrar to create glue records and change the registrar's name servers:

1. Add glue records:
   + **If you're updating the domain that has the same domain name as the white\-label name servers** – Create four glue records for which the names and IP addresses match the values that you got in step 4\. Include both the IPv4 and the IPv6 address for a white\-label name server in the corresponding glue record, for example:

     **ns1\.example\.com** – IP addresses = 192\.0\.2\.117 and 2001:db8:85a3::8a2e:370:7334

     Registrars use a variety of terminology for glue records\. You might also see this referred to as registering new name servers or something similar\.
   + **If you're updating another domain** – Skip to step 2 in this procedure\.

1. Change the name servers for the domain to the names of your white\-label name servers\.

If you're using Amazon Route 53 as your DNS service, see [Adding or changing name servers and glue records for a domain](domain-name-servers-glue-records.md)\.

## Step 8: Monitor traffic for the website or application<a name="white-label-name-servers-monitor-traffic"></a>

Monitor the traffic for the website or application for which you created glue records and changed name servers in Step 7:
+ **If the traffic stops** – Use the method provided by the registrar to change the name servers for the domain back to the previous Route 53 name servers\. These are the name servers that you made note of in step 6b\. Then determine what went wrong\.
+ **If the traffic is unaffected** – Repeat Step 6 through Step 8 for the rest of the hosted zones for which you want to use the same white\-label name servers\. 

## Step 9: Change TTLs back to their original values<a name="white-label-name-servers-change-ttls-back"></a>

For all of the hosted zones that are now using white\-label name servers, change the following values:
+ Change the TTL for the NS record for the hosted zone to a more typical value for NS records, for example, 172800 seconds \(two days\)\.
+ Change the minimum TTL for the SOA record for the hosted zone to a more typical value for SOA records, for example, 900 seconds\. This is the last value in the SOA record\.

## Step 10: \(Optional\) contact recursive DNS services<a name="white-label-name-servers-contact-recursive-dns-services"></a>

*Optional* If you're using Amazon Route 53 geolocation routing, contact the recursive DNS services that support the edns\-client\-subnet extension of EDNS0, and give them the names of your white\-label name servers\. This ensures that these DNS services will continue to route DNS queries to the optimal Route 53 location based on the approximate geographical location that the query came from\.