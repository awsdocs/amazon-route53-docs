# Routing traffic to a website that is hosted in an Amazon S3 bucket<a name="RoutingToS3Bucket"></a>

Amazon Simple Storage Service \(Amazon S3\) provides secure, durable, highly scalable [cloud storage](https://aws.amazon.com/what-is-cloud-storage/)\. You can configure an S3 bucket to host a static website that can include web pages and client\-side scripts\. \(S3 doesn't support server\-side scripting\.\)

To route domain traffic to an S3 bucket, use Amazon Route 53 to create an [alias record](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) that points to your bucket\. An alias record is a Route 53 extension to DNS\. It's similar to a CNAME record, except you can create an alias record both for the root domain, such as example\.com, and for subdomains, such as www\.example\.com\. You can create CNAME records only for subdomains\. 

**Note**  
Route 53 doesn't charge for alias queries to S3 buckets or other AWS resources\.

## Prerequisites<a name="routing-to-s3-bucket-prereqs"></a>

Before you get started, you need the following\. If you're new to Amazon Route 53 or S3, see [Getting started with Amazon Route 53](getting-started.md), which guides you through the entire process, including registering a domain name, and creating and configuring an S3 bucket\.
+ An S3 bucket and, if you want to use SSL/TLS, a CloudFront distribution:  
**If you don't want to use SSL/TLS to encrypt traffic**  
An S3 bucket that's configured to host a static website\. For more information, see [Configure a bucket for website hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\.  
The bucket must have the same name as your domain or subdomain\. For example, if you want to use the subdomain acme\.example\.com, the name of the bucket must be acme\.example\.com\.
You can route traffic for a domain and its subdomains, such as example\.com and www\.example\.com, to a single bucket\. Create a bucket for the domain and each subdomain, and configure all but one of the buckets to redirect traffic to the remaining bucket\. For more information, see [Getting started with Amazon Route 53](getting-started.md)\.  
**If you do want to use SSL/TLS to encrypt traffic**  
An S3 bucket that's *not* configured to host a static website, and a CloudFront distribution that's configured to use your S3 bucket as the origin\. An S3 bucket that's configured as a website endpoint doesn't support SSL/TLS, so you need to route traffic to the CloudFront distribution and use the S3 bucket as the origin for the distribution\. For more information, see [Requiring HTTPS for communication between viewers and CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-viewers-to-cloudfront.html) in the *Amazon CloudFront Developer Guide*\.
+ A registered domain name\. You can use Route 53 as your domain registrar, or you can use a different registrar\.
+ Route 53 as the DNS service for the domain\. If you register your domain name by using Route 53, we automatically configure Route 53 as the DNS service for the domain\. 

  For information about using Route 53 as the DNS service provider for your domain, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

## Configuring Amazon Route 53 to route traffic to an S3 Bucket<a name="routing-to-s3-bucket-configuring"></a>

To configure Amazon Route 53 to route traffic to an S3 bucket that is configured to host a static website, perform the following procedure\.<a name="routing-to-s3-bucket-procedure"></a>

**To route traffic to an S3 bucket**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that has the domain name that you want to use to route traffic to your S3 bucket\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Enter the domain name that you want to use to route traffic to your S3 bucket\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to route traffic to your bucket, enter **acme**\.  
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
In the **S3 website endpoints** section of the list, choose the bucket that has the same name that you specified for **Name**\.  
The **Alias Target** list includes a bucket only if the bucket meets the following requirements:  
   + The name of the bucket is the same as the name of the record that you're creating\.
   + The bucket is configured as a website endpoint\.
   + The bucket was created by the current AWS account\.

     If you created the bucket using a different AWS account, enter the name of the Region that you created your S3 bucket in\. For the correct format for the Region name, see the **Website Endpoint** column in the table [Amazon S3 website endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html#s3_website_region_endpoints) in the *Amazon Web Services General Reference*\.  
**Routing Policy**  
Choose the applicable routing policy\. For more information, see [Choosing a routing policy](routing-policy.md)\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your S3 bucket by using the name of the alias record that you created in this procedure\. 