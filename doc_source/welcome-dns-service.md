# How internet traffic is routed to your website or web application<a name="welcome-dns-service"></a>

All computers on the internet, from your smart phone or laptop to the servers that serve content for massive retail websites, communicate with one another by using numbers\. These numbers, known as *IP addresses*, are in one of the following formats:
+ Internet Protocol version 4 \(IPv4\) format, such as 192\.0\.2\.44
+ Internet Protocol version 6 \(IPv6\) format, such as 2001:0db8:85a3:0000:0000:abcd:0001:2345

When you open a browser and go to a website, you don't have to remember and enter a long string of characters like that\. Instead, you can enter a domain name like example\.com and still end up in the right place\. A DNS service such as Amazon Route 53 helps to make that connection between domain names and IP addresses\.

**Topics**
+ [Overview of how you configure Amazon Route 53 to route internet traffic for your domain](#welcome-dns-service-how-to-configure)
+ [How Amazon Route 53 routes traffic for your domain](#welcome-dns-service-how-route-53-routes-traffic)

## Overview of how you configure Amazon Route 53 to route internet traffic for your domain<a name="welcome-dns-service-how-to-configure"></a>

Here's an overview of how to use the Amazon Route 53 console to register a domain name and configure Route 53 to route internet traffic to your website or web application\. 

1. You register the domain name that you want your users to use to access your content\. For an overview, see [How domain registration works](welcome-domain-registration.md)\.

1. After you register your domain name, Route 53 automatically creates a public hosted zone that has the same name as the domain\. For more information, see [Working with public hosted zones](AboutHZWorkingWith.md)\.

1. To route traffic to your resources, you create *records*, also known as *resource record sets*, in your hosted zone\. Each record includes information about how you want to route traffic for your domain, such as the following:  
**Name**  
The name of the record corresponds with the domain name \(example\.com\) or subdomain name \(www\.example\.com, retail\.example\.com\) that you want Route 53 to route traffic for\.   
The name of every record in a hosted zone must end with the name of the hosted zone\. For example, if the name of the hosted zone is example\.com, all record names must end in example\.com\. The Route 53 console does this for you automatically\.  
**Type**  
The record type usually determines the type of resource that you want traffic to be routed to\. For example, to route traffic to an email server, you specify MX for Type\. To route traffic to a web server that has an IPv4 IP address, you specify A for Type\.  
**Value**  
Value is closely related to Type\. If you specify MX for Type, you specify the names of one or more email servers for Value\. If you specify A for Type, you specify an IP address in IPv4 format, such as 192\.0\.2\.136\.

For more information about records, see [Working with records](rrsets-working-with.md)\.

You can also create special Route 53 records, called alias records, that route traffic to Amazon S3 buckets, Amazon CloudFront distributions, and other AWS resources\. For more information, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md) and [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.

For more information about routing internet traffic to your resources, see [Configuring Amazon Route 53 as your DNS service](dns-configuring.md)\.

## How Amazon Route 53 routes traffic for your domain<a name="welcome-dns-service-how-route-53-routes-traffic"></a>

After you configure Amazon Route 53 to route your internet traffic to your resources, such as web servers or Amazon S3 buckets, here's what happens in just a few milliseconds when someone requests content for www\.example\.com:

![\[Conceptual graphic that shows how the Domain Name System and Route 53 route internet traffic to the resources for www.example.com.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/how-route-53-routes-traffic.png)

1. A user opens a web browser, enters www\.example\.com in the address bar, and presses Enter\.

1. The request for www\.example\.com is routed to a DNS resolver, which is typically managed by the user's internet service provider \(ISP\), such as a cable internet provider, a DSL broadband provider, or a corporate network\.

1. The DNS resolver for the ISP forwards the request for www\.example\.com to a DNS root name server\. 

1. The DNS resolver forwards the request for www\.example\.com again, this time to one of the TLD name servers for \.com domains\. The name server for \.com domains responds to the request with the names of the four Route 53 name servers that are associated with the example\.com domain\. 

   The DNS resolver caches \(stores\) the four Route 53 name servers\. The next time someone browses to example\.com, the resolver skips steps 3 and 4 because it already has the name servers for example\.com\. The name servers are typically cached for two days\.

1. The DNS resolver chooses a Route 53 name server and forwards the request for www\.example\.com to that name server\.

1. The Route 53 name server looks in the example\.com hosted zone for the www\.example\.com record, gets the associated value, such as the IP address for a web server, 192\.0\.2\.44, and returns the IP address to the DNS resolver\.

1. The DNS resolver finally has the IP address that the user needs\. The resolver returns that value to the web browser\.
**Note**  
The DNS resolver also caches the IP address for example\.com for an amount of time that you specify so that it can respond more quickly the next time someone browses to example\.com\. For more information, see [time to live (TTL)](route-53-concepts.md#route-53-concepts-time-to-live)\.

1. The web browser sends a request for www\.example\.com to the IP address that it got from the DNS resolver\. This is where your content is, for example, a web server running on an Amazon EC2 instance or an Amazon S3 bucket that's configured as a website endpoint\.

1. The web server or other resource at 192\.0\.2\.44 returns the web page for www\.example\.com to the web browser, and the web browser displays the page\.