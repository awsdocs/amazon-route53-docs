# Routing traffic to an Amazon CloudFront web distribution by using your domain name<a name="routing-to-cloudfront-distribution"></a>

If you want to speed up delivery of your web content, you can use Amazon CloudFront, the AWS content delivery network \(CDN\)\. CloudFront can deliver your entire website—including dynamic, static, streaming, and interactive content—by using a global network of edge locations\. Requests for your content are automatically routed to the edge location that gives your users the lowest latency\. 

**Note**  
You can route traffic to a CloudFront distribution only for public hosted zones\.

To use CloudFront to distribute your content, you create a web distribution and specify settings such as the Amazon S3 bucket or HTTP server that you want CloudFront to get your content from, whether you want only selected users to have access to your content, and whether you want to require users to use HTTPS\.

When you create a web distribution, CloudFront assigns a domain name to the distribution, such as d111111abcdef8\.cloudfront\.net\. You can use this domain name in the URLs for your content, for example:

`http://d111111abcdef8.cloudfront.net/logo.jpg`

Alternatively, you might prefer to use your own domain name in URLs, for example:

`http://example.com/logo.jpg`

If you want to use your own domain name, use Amazon Route 53 to create an [alias record](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) that points to your CloudFront distribution\. An alias record is a Route 53 extension to DNS\. It's similar to a CNAME record, but you can create an alias record both for the root domain, such as example\.com, and for subdomains, such as www\.example\.com\. \(You can create CNAME records only for subdomains\.\) When Route 53 receives a DNS query that matches the name and type of an alias record, Route 53 responds with the domain name that is associated with your distribution\. 

**Note**  
Route 53 doesn't charge for alias queries to CloudFront distributions or other AWS resources\.

## Prerequisites<a name="routing-to-cloudfront-distribution-prereqs"></a>

Before you get started, you need the following:
+ A CloudFront web distribution\. The distribution must include an alternate domain name that matches the domain name that you want to use for your URLs instead of the domain name that CloudFront assigned to your distribution\.

  For example, if you want the URLs for your content to contain the domain name **example\.com**, the **Alternate Domain Name** field for the distribution must include **example\.com**\.

  For more information, see the following documentation in the *Amazon CloudFront Developer Guide*:
  + [Task list for creating a web distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating.html)
  + [Creating or updating a web distribution using the CloudFront console](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating-console.html)
+ A registered domain name\. You can use Amazon Route 53 as your domain registrar, or you can use a different registrar\.
+ Route 53 as the DNS service for the domain\. If you register your domain name by using Route 53, we automatically configure Route 53 as the DNS service for the domain\. 

  For information about using Route 53 as the DNS service provider for your domain, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

## Configuring Amazon Route 53 to route traffic to a CloudFront web distribution<a name="routing-to-cloudfront-distribution-config"></a>

To configure Amazon Route 53 to route traffic to a CloudFront web distribution, perform the following procedure\.

**Note**  
Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your CloudFront distribution by using the name of the alias record that you create in this procedure\. <a name="routing-to-cloudfront-distribution-procedure"></a>

**To route traffic to a CloudFront web distribution**

1. Get the domain name that CloudFront assigned to your web distribution, and determine whether IPv6 is enabled:

   1. Sign in to the AWS Management Console and open the CloudFront console at [https://console\.aws\.amazon\.com/cloudfront/](https://console.aws.amazon.com/cloudfront/)\.

   1. Choose the name of the distribution that you want to route traffic to\.

   1. On the **General** tab, get the value of the **Domain Name** field\.

   1. Check the **IPv6** field to see whether IPv6 is enabled for the distribution\. If IPv6 is enabled, you'll need to create two alias records for the distribution, one to route IPv4 traffic to the distribution, and one to route IPv6 traffic\.

      For more information, see [Enable IPv6](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesEnableIPv6) in the topic [Values that you specify when you create or update a web distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html) in the *Amazon CloudFront Developer Guide*\.

1. If you haven't already, add one or more alternate domain names to your CloudFront distribution\. These are the domain names \(such as example\.com\) and subdomain names \(such as acme\.example\.com\) that you want to use for your URLs instead of the domain name that CloudFront assigned to your distribution\.

   For more information, see [Using alternate domain names \(CNAMEs\)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) in the *Amazon CloudFront Developer Guide*\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone for the domain that you want to use to route traffic to your CloudFront distribution\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the domain name that you want to use to route traffic to your CloudFront distribution\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use **acme\.example\.com** to route traffic to your distribution, enter **acme**\.  
**Type**  
Choose **A – IPv4 address**\.  
If IPv6 is enabled for the distribution and you're creating a second record, choose **AAAA – IPv6 address**\.   
**Alias**  
Choose **Yes**\.  
**Alias Target**  
In the **CloudFront distributions** section, choose the name that CloudFront assigned to the distribution when you created it\. This is the value that you got in step 1\.  
**Routing Policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

1. If IPv6 is enabled for the distribution, repeat steps 6 through 8\. Specify the same settings except for the **Type** field, as explained in step 7\.