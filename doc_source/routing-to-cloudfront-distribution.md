# Routing traffic to an Amazon CloudFront distribution by using your domain name<a name="routing-to-cloudfront-distribution"></a>

You can use Amazon CloudFront, the AWS content delivery network \(CDN\), if you want to speed up delivery of your web content\. CloudFront can deliver your entire website—including dynamic, static, streaming, and interactive content—by using a global network of edge locations\. Requests for your content are automatically routed to the edge location that gives your users the lowest latency\. 

**Note**  
You can route traffic to a CloudFront distribution only for public hosted zones\.

To use CloudFront to distribute your content, create a distribution and specify settings such as the Amazon S3 bucket or HTTP server that you want CloudFront to get your content from, whether you want only selected users to have access to your content, and whether you want users to use HTTPS\.

When you create a distribution, CloudFront assigns a domain name to the distribution, such as d111111abcdef8\.cloudfront\.net\. You can use this domain name in the URLs for your content, for example:

`http://d111111abcdef8.cloudfront.net/logo.jpg`

Alternatively, you can use your own domain name in URLs, for example:

`http://example.com/logo.jpg`

If you want to use your own domain name, use Amazon Route 53 to create an [alias record](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) that points to your CloudFront distribution\. An alias record is a Route 53 extension to DNS\. It's similar to a CNAME record, but you can create an alias record both for the root domain, such as example\.com, and for subdomains, such as www\.example\.com\. \(You can create CNAME records only for subdomains\.\) When Route 53 receives a DNS query that matches the name and type of an alias record, Route 53 responds with the domain name that is associated with your distribution\. 

**Note**  
Route 53 doesn't charge for alias queries to CloudFront distributions or other AWS resources\.

## Prerequisites<a name="routing-to-cloudfront-distribution-prereqs"></a>

To get started, you need the following:

1. A registered domain name\. You can use Amazon Route 53 as your domain registrar or you can use a different registrar\.

1. Route 53 as the DNS service for the domain\. If you register your domain name by using Route 53, we automatically configure Route 53 as the DNS service for the domain\. 

   For information about using Route 53 as the DNS service provider for your domain, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

1. Request a public certificate so that Amazon CloudFront distributions require HTTPS\. For more information, see [Step 2: Request a public certificate](getting-started-cloudfront-overview.md#getting-started-cloudfront-request-certificate) and [DNS validation in the AWS Certificate Manager](https://docs.aws.amazon.com/acm/latest/userguide/dns-validation.html) in the *AWS Certificate Manager User Guide\.*

1. A CloudFront distribution\. The distribution must include an alternate domain name that matches the domain name that you want to use for your URLs instead of the domain name that CloudFront assigned to your distribution\.

   For example, if you want the URLs for your content to contain the domain name **example\.com**, the **Alternate Domain Name** field for the distribution must include **example\.com**\.

   For more information, see the following documentation in the *Amazon CloudFront Developer Guide*:
   + [Task list for creating a distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating.html)
   + [Creating or updating a distribution using the CloudFront console](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating-console.html)

## Configuring Amazon Route 53 to route traffic to a CloudFront distribution<a name="routing-to-cloudfront-distribution-config"></a>

To configure Amazon Route 53 to route traffic to a CloudFront distribution, perform the following procedure\.

**Note**  
Changes generally propagate to all Route 53 servers within 60 seconds\. When the changes propagate, you'll be able to route traffic to your CloudFront distribution by using the name of the alias record that you create in this procedure\. <a name="routing-to-cloudfront-distribution-procedure"></a>

**To route traffic to a CloudFront distribution**

1. Get the domain name that CloudFront assigned to your distribution and determine whether IPv6 is enabled:

   1. Sign in to the AWS Management Console and open the CloudFront console at [https://console.aws.amazon.com/cloudfront/v3/home](https://console.aws.amazon.com/cloudfront/v3/home)\.

   1. in the **ID** column, select the linked name of the distribution that you want to route traffic to \(not the check box\)\.

   1. On the **General** tab, get the value of the **Distribution domain name** field\.

   1. On the **General** tab, in the **Settings** section, choose edit and scroll to check the **IPv6** field to see whether IPv6 is enabled for the distribution\. If IPv6 is enabled, you'll need to create two alias records for the distribution, one to route IPv4 traffic to the distribution, and one to route IPv6 traffic\. Choose **Cancel**\.

      For more information, see [Enable IPv6](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesEnableIPv6) in the topic [Values that you specify when you create or update a distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html) in the *Amazon CloudFront Developer Guide*\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. Choose the linked name of the hosted zone for the domain that you want to use to route traffic to your CloudFront distribution\.

1. Choose **Create record**\.

   You can use the wizard to create the records or choose **Switch to quick create**\.

1. Specify the following values:  
**Routing policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.  
**Record name**  
Enter the domain name that you want to use to route traffic to your CloudFront distribution\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use **acme\.example\.com** to route traffic to your distribution, enter **acme**\.  
**Alias**  
If you are using the **Quick create** record creation method, turn on **Alias**\.  
You must create an Alias record for the CloudFront distribution to work\.  
**Value/Route traffic to**  
Choose **Alias to CloudFront distributions**\. The us\-east\-1 Region is selected by default\. Choose the domain name that CloudFront assigned to the distribution when you created it\. This is the value that you got in step 1\.  
**Record type**  
Choose **A – IPv4 address**\.  
If IPv6 is enabled for the distribution and you're creating a second record, choose **AAAA – IPv6 address**\.   
**Evaluate target health**  
Accept the default value of **No**\.

1. Choose **Create records**\.

1. If IPv6 is enabled for the distribution, repeat steps 6 through 8\. Specify the same settings except for the **Record type** field, as explained in step 6\.
