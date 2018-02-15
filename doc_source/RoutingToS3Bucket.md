# Routing Traffic to a Website that Is Hosted in an Amazon S3 Bucket<a name="RoutingToS3Bucket"></a>

Amazon Simple Storage Service \(Amazon S3\) provides secure, durable, highly scalable [cloud storage](https://aws.amazon.com/what-is-cloud-storage/)\. You can configure an S3 bucket to host a static website that can include web pages and client\-side scripts\. \(S3 doesn't support server\-side scripting\.\)

To route domain traffic to an S3 bucket, use Amazon Route 53 to create an [alias record](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) that points to your bucket\. An alias record is a Route 53 extension to DNS\. It's similar to a CNAME record, except you can create an alias record both for the root domain, such as example\.com, and for subdomains, such as www\.example\.com\. You can create CNAME records only for subdomains\. 

**Note**  
Route 53 doesn't charge for alias queries to S3 buckets or other AWS resources\.

## Prerequisites<a name="routing-to-s3-bucket-prereqs"></a>

Before you get started, you need the following\. If you're new to Amazon Route 53 or S3, see [Getting Started with Amazon Route 53](getting-started.md), which guides you through the entire process, including registering a domain name, and creating and configuring an S3 bucket\.

+ An S3 bucket that is configured to host a static website\. For more information, see [Configure a Bucket for Website Hosting](http://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\.
**Important**  
The bucket must have the same name as your domain or subdomain\. For example, if you want to use the subdomain acme\.example\.com, the name of the bucket must be acme\.example\.com\.

  You can route traffic for a domain and its subdomains, such as example\.com and www\.example\.com, to a single bucket\. Create a bucket for the domain and each subdomain, and configure all but one of the buckets to redirect traffic to the remaining bucket\. For more information, see [Getting Started with Amazon Route 53](getting-started.md)\.

+ A registered domain name\. You can use Route 53 as your domain registrar, or you can use a different registrar\.

+ Route 53 as the DNS service for the domain\. If you register your domain name by using Route 53, we automatically configure Route 53 as the DNS service for the domain\. 

  For information about migrating DNS service to Route 53, see [Using Amazon Route 53 as the DNS Service for Subdomains Without Migrating the Parent Domain](creating-migrating.md)\.

## Configuring Amazon Route 53 to Route Traffic to an S3 Bucket<a name="routing-to-s3-bucket-configuring"></a>

To configure Amazon Route 53 to route traffic to an S3 bucket that is configured to host a static website, perform the following procedure\.

**To route traffic to an S3 bucket**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that has the domain name that you want to use to route traffic to your S3 bucket\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Type the domain name that you want to use to route traffic to your S3 bucket\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to route traffic to your bucket, type **acme**\.  
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
In the **S3 website endpoints** section of the list, choose the bucket that has the same name that you specified for **Name**\.  
**Routing Policy**  
Accept the default value of **Simple**\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your S3 bucket by using the name of the alias record that you created in this procedure\. 