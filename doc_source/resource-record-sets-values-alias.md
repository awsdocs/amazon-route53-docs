# Values for alias records<a name="resource-record-sets-values-alias"></a>

When you create alias records, you specify the following values\. For more information, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**Topics**
+ [Name](#rrsets-values-alias-name)
+ [Type](#rrsets-values-alias-type)
+ [Alias](#rrsets-values-alias-alias)
+ [Alias target](#rrsets-values-alias-alias-target)
+ [Alias hosted zone ID](#rrsets-values-alias-hosted-zone-id)
+ [Routing policy](#rrsets-values-alias-routing-policy)
+ [Evaluate target health](#rrsets-values-alias-evaluate-target-health)

## Name<a name="rrsets-values-alias-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

**CNAME records**  
If you're creating a record that has a value of **CNAME** for **Type**, the name of the record can't be the same as the name of the hosted zone\.

**Aliases to CloudFront distributions and Amazon S3 buckets**  
The value that you specify depends in part on the AWS resource that you're routing traffic to:  
+ **CloudFront distribution** – Your distribution must include an alternate domain name that matches the name of the record\. For example, if the name of the record is **acme\.example\.com**, your CloudFront distribution must include **acme\.example\.com** as one of the alternate domain names\. For more information, see [Using alternate domain names \(CNAMEs\)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) in the *Amazon CloudFront Developer Guide*\. 
+ **Amazon S3 bucket** – The name of the record must match the name of your Amazon S3 bucket\. For example, if the name of your bucket is **acme\.example\.com**, the name of this record must also be **acme\.example\.com**\.

  In addition, you must configure the bucket for website hosting\. For more information, see [Configure a bucket for website hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\. 

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an asterisk \(\*\) in the names of hosted zones and records](DomainNameFormat.md#domain-name-format-asterisk)\.

## Type<a name="rrsets-values-alias-type"></a>

The DNS record type\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

Select the applicable value based on the AWS resource that you're routing traffic to:

**API Gateway custom regional API or edge\-optimized API**  
Select **A — IPv4 address**\.

**Amazon VPC interface endpoints**  
Select **A — IPv4 address**\.

**CloudFront distribution**  
Select **A — IPv4 address**\.  
If IPv6 is enabled for the distribution, create two records, one with a value of **A — IPv4 address** for **Type**, and one with a value of **AAAA — IPv6 address**\.

**Elastic Beanstalk environment that has regionalized subdomains**  
Select **A — IPv4 address**

**ELB load balancer**  
Select **A — IPv4 address** or **AAAA — IPv6 address**

**Amazon S3 bucket**  
Select **A — IPv4 address**

**Another record in this hosted zone**  
Select the type of the record that you're creating the alias for\. All types are supported except **NS** and **SOA**\.  
If you're creating an alias record that has the same name as the hosted zone \(known as the *zone apex*\), you can't route traffic to a record for which the value of **Type** is **CNAME**\. This is because the alias record must have the same type as the record you're routing traffic to, and creating a CNAME record for the zone apex isn't supported even for an alias record\. 

## Alias<a name="rrsets-values-alias-alias"></a>

Select **Yes**\. 

## Alias target<a name="rrsets-values-alias-alias-target"></a>

The value that you choose from the list or that you type in the field depends on the AWS resource that you're routing traffic to\.

**Important**  
If you used the same AWS account to create your hosted zone and the resource that you're routing traffic to, and if your resource doesn't appear in the **Alias Target** list, check the following:  
Confirm that you chose a supported value for **Type**\. Supported values are specific to the resource that you're routing traffic to\. For example, to route traffic to an S3 bucket, you must choose **A — IPv4 address** for **Type**\.
Confirm that the account has the IAM permissions that are required to list the applicable resources\. For example, for CloudFront distributions to appear in the **Alias Target** list, the account must have permission to perform the following action: `cloudfront:ListDistributions`\.  
For an example IAM policy, see [Permissions required to use the Amazon Route 53 console](access-control-managing-permissions.md#console-required-permissions)\.
If you used different AWS accounts to create the hosted zone and the resource, the **Alias Target** list doesn't display your resource\. See the following documentation for your resource type to determine what value to type in **Alias Target**\.

**API Gateway custom regional APIs and edge\-optimized APIs**  
For API Gateway custom regional APIs and edge\-optimized APIs, do one of the following:  
+ **If you used the same account to create your Route 53 hosted zone and your API** – Choose **Alias Target**, and then choose an API from the list\. If you have a lot of APIs, you can enter the first few characters of the API endpoint to filter the list\.
**Note**  
The name of this record must match a custom domain name for your API, such as **api\.example\.com**\.
+ **If you used different accounts to create your Route 53 hosted zone and your API** – Enter the API endpoint for the API, such as **api\.example\.com**\.

  If you used one AWS account to create the current hosted zone and a different account to create an API, the API won't appear in the **Alias Targets** list under **API Gateway APIs**\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your APIs, the **Alias Targets** list shows **No Targets Available** under **API Gateway APIs**\.

**CloudFront Distributions**  
For CloudFront distributions, do one of the following:  
+ **If you used the same account to create your Route 53 hosted zone and your CloudFront distribution** – Choose **Alias Target** and choose a distribution from the list\. If you have a lot of distributions, you can enter the first few characters of the domain name for your distribution to filter the list\.

  If your distribution doesn't appear in the list, note the following:
  + The name of this record must match an alternate domain name in your distribution\.
  + If you just added an alternate domain name to your distribution, it may take 15 minutes for your changes to propagate to all CloudFront edge locations\. Until changes have propagated, Route 53 can't know about the new alternate domain name\.
+ **If you used different accounts to create your Route 53 hosted zone and your distribution** – Enter the CloudFront domain name for the distribution, such as **d111111abcdef8\.cloudfront\.net**\.

  If you used one AWS account to create the current hosted zone and a different account to create a distribution, the distribution will not appear in the **Alias Targets** list\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your distributions, the **Alias Targets** list shows **No Targets Available** under **CloudFront Distributions**\.
Do not route queries to a CloudFront distribution that has not propagated to all edge locations, or your users won't be able to access the applicable content\. 
Your CloudFront distribution must include an alternate domain name that matches the name of the record\. For example, if the name of the record is **acme\.example\.com**, your CloudFront distribution must include **acme\.example\.com** as one of the alternate domain names\. For more information, see [Using alternate domain names \(CNAMEs\)](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) in the *Amazon CloudFront Developer Guide*\.  
If IPv6 is enabled for the distribution, create two records, one with a value of **A — IPv4 address** for **Type**, and one with a value of **AAAA — IPv6 address**\.

**Elastic Beanstalk environments that have regionalized subdomains**  
If the domain name for your Elastic Beanstalk environment includes the region that you deployed the environment in, you can create an alias record that routes traffic to the environment\. For example, the domain name `my-environment.us-west-2.elasticbeanstalk.com` is a regionalized domain name\.  
For environments that were created before early 2016, the domain name doesn't include the region\. To route traffic to these environments, you must create a CNAME record instead of an alias record\. Note that you can't create a CNAME record for the root domain name\. For example, if your domain name is example\.com, you can create a record that routes traffic for acme\.example\.com to your Elastic Beanstalk environment, but you can't create a record that routes traffic for example\.com to your Elastic Beanstalk environment\.
For Elastic Beanstalk environments that have regionalized subdomains, do one of the following:  
+ **If you used the same account to create your Route 53 hosted zone and your Elastic Beanstalk environment** – Choose **Alias Target**, and then choose an environment from the list\. If you have a lot of environments, you can enter the first few characters of the CNAME attribute for the environment to filter the list\.
+ **If you used different accounts to create your Route 53 hosted zone and your Elastic Beanstalk environment** – Enter the CNAME attribute for the Elastic Beanstalk environment\.

**ELB Load Balancers**  
For ELB load balancers, do one of the following:  
+ **If you used the same account to create your Route 53 hosted zone and your load balancer** – Choose **Alias Target** and choose a load balancer from the list\. If you have a lot of load balancers, you can enter the first few characters of the DNS name to filter the list\.
+ **If you used different accounts to create your Route 53 hosted zone and your load balancer** – Enter the value that you got in the procedure [Getting the DNS name for an ELB load balancer](resource-record-sets-creating.md#resource-record-sets-elb-dns-name-procedure)\.

  If you used one AWS account to create the current hosted zone and a different account to create a load balancer, the load balancer will not appear in the **Alias Targets** list\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your load balancers, the **Alias Targets** list shows **No Targets Available** under **Elastic Load Balancers**\.
In either case, the console prepends **dualstack\.** to the DNS name\. When a client, such as a web browser, requests the IP address for your domain name \(example\.com\) or subdomain name \(www\.example\.com\), the client can request an IPv4 address \(an A record\), an IPv6 address \(a AAAA record\), or both IPv4 and IPv6 addresses \(in separate requests\)\. The **dualstack\.** designation allows Route 53 to respond with the appropriate IP address for your load balancer based on which IP address format the client requested\.

**AWS Global Accelerator accelerators**  
For AWS Global Accelerator accelerators, enter the DNS name for the accelerator\. You can enter the DNS name of an accelerator that you created using the current AWS account or using a different AWS account\. 

**Amazon S3 Buckets**  
For Amazon S3 buckets that are configured as website endpoints, do one of the following:  
+ **If you used the same account to create your Route 53 hosted zone and your Amazon S3 bucket** – Choose **Alias Target** and choose a bucket from the list\. If you have a lot of buckets, you can enter the first few characters of the DNS name to filter the list\.

  The value of **Alias Target** changes to the Amazon S3 website endpoint for your bucket\.
+ **If you used different accounts to create your Route 53 hosted zone and your Amazon S3 bucket** – Enter the name of the region that you created your S3 bucket in\. Use the value that appears in the **Website Endpoint** column in the table [Amazon S3 website endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html#s3_website_region_endpoints) in the *Amazon Web Services General Reference*\.

  If you used AWS accounts other than the current account to create your Amazon S3 buckets, the bucket won't appear in the **Alias Targets** list\.
You must configure the bucket for website hosting\. For more information, see [Configure a bucket for website hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\.  
The name of the record must match the name of your Amazon S3 bucket\. For example, if the name of your Amazon S3 bucket is **acme\.example\.com**, the name of this record must also be **acme\.example\.com**\.  
In a group of weighted alias, latency alias, failover alias, or geolocation alias records, you can create only one record that routes queries to an Amazon S3 bucket because the name of the record must match the name of the bucket and bucket names must be globally unique\.

**Amazon VPC interface endpoints**  
For Amazon VPC interface endpoints, do one of the following:  
+ **If you used the same account to create your Route 53 hosted zone and your interface endpoint** – Choose **Alias Target**, and then choose an interface endpoint from the list\. If you have a lot of interface endpoints, you can enter the first few characters of the DNS hostname to filter the list\.
+ **If you used different accounts to create your Route 53 hosted zone and your interface endpoint** – Enter the DNS hostname for the interface endpoint, such as **vpce\-123456789abcdef01\-example\-us\-east\-1a\.elasticloadbalancing\.us\-east\-1\.vpce\.amazonaws\.com**\.

  If you used one AWS account to create the current hosted zone and a different account to create an interface endpoint, the interface endpoint won't appear in the **Alias Targets** list under **VPC Endpoints**\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your interface endpoints, the **Alias Targets** list shows **No Targets Available** under **VPC Endpoints**\.

**Records in this Hosted Zone**  
For records in this hosted zone, choose **Alias Target** and choose the applicable record\. If you have a lot of records, you can enter the first few characters of the name to filter the list\.  
If the hosted zone contains only the default NS and SOA records, the **Alias Targets** list shows **No Targets Available**\.  
If you're creating an alias record that has the same name as the hosted zone \(known as the *zone apex*\), you can't choose a record for which the value of **Type** is **CNAME**\. This is because the alias record must have the same type as the record you're routing traffic to, and creating a CNAME record for the zone apex isn't supported even for an alias record\. 

## Alias hosted zone ID<a name="rrsets-values-alias-hosted-zone-id"></a>

This value appears automatically based on the value that you selected or entered for **Alias Target**\.

## Routing policy<a name="rrsets-values-alias-routing-policy"></a>

Select **Simple**\.

## Evaluate target health<a name="rrsets-values-alias-evaluate-target-health"></a>

When the value of **Routing Policy** is **Simple**, choose **No**\. If you have only one record that has a given name and type, Route 53 responds to DNS queries using the values in that record regardless of whether the resource is healthy\.