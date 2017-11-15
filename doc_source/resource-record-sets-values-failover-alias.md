# Values for Failover Alias Resource Record Sets<a name="resource-record-sets-values-failover-alias"></a>

When you create failover alias resource record sets, you specify the following values:

**Note**  
For information about creating failover resource record sets in a private hosted zone, see [Configuring Failover in a Private Hosted Zone](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover-private-hosted-zones.html) in the *Amazon Route 53 Developer Guide*\.


+ [Name](#rrsets-values-failover-alias-name)
+ [Type](#rrsets-values-failover-alias-type)
+ [Alias](#rrsets-values-failover-alias-alias)
+ [Alias Target](#rrsets-values-failover-alias-alias-target)
+ [Alias Hosted Zone ID](#rrsets-values-failover-alias-hosted-zone-id)
+ [Routing Policy](#rrsets-values-failover-alias-routing-policy)
+ [Failover Record Type](#rrsets-values-failover-alias-failover-record-type)
+ [Set ID](#rrsets-values-failover-alias-set-id)
+ [Evaluate Target Health](#rrsets-values-failover-alias-evaluate-target-health)
+ [Associate with Health Check/Health Check to Associate](#rrsets-values-failover-alias-associate-with-health-check)

## Name<a name="rrsets-values-failover-alias-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a resource record set that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

Enter the same name for both of the resource record sets in the group of failover resource record sets\. 

**CNAME resource record sets**  
If you're creating a resource record set that has a value of **CNAME** for **Type**, the name of the resource record set can't be the same as the name of the hosted zone\.

**Aliases to CloudFront distributions and Amazon S3 buckets**  
The value that you specify depends in part on the AWS resource that you're routing traffic to:  

+ **CloudFront distribution** – Your distribution must include an alternate domain name that matches the name of the resource record set\. For example, if the name of the resource record set is **acme\.example\.com**, your CloudFront distribution must include **acme\.example\.com** as one of the alternate domain names\. For more information, see [Using Alternate Domain Names \(CNAMEs\)](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) in the *Amazon CloudFront Developer Guide*\.

+ **Amazon S3 bucket** – The name of the resource record set must match the name of your Amazon S3 bucket\. For example, if the name of your bucket is **acme\.example\.com**, the name of this resource record set must also be **acme\.example\.com**\.

  In addition, you must configure the bucket for website hosting\. For more information, see [Configure a Bucket for Website Hosting](http://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\.

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an Asterisk \(\*\) in the Names of Hosted Zones and Resource Record Sets](DomainNameFormat.md#domain-name-format-asterisk)\.

## Type<a name="rrsets-values-failover-alias-type"></a>

The DNS record type\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

Select the applicable value based on the AWS resource that you're routing traffic to:

**CloudFront distribution**  
Select **A — IPv4 address**\.  
If IPv6 is enabled for the distribution, create two resource record sets, one with a value of **A — IPv4 address** for **Type**, and one with a value of **AAAA — IPv6 address**\.

**Elastic Beanstalk environment that has regionalized subdomains**  
Select **A — IPv4 address**

**ELB load balancer**  
Select **A — IPv4 address** or **AAAA — IPv6 address**

**Amazon S3 bucket**  
Select **A — IPv4 address**

**Another resource record set in this hosted zone**  
Select the type of the resource record set that you're creating the alias for\. All types are supported except **NS** and **SOA**\.

Select any value except **NS** or **SOA**\. Select the same value for both the primary and secondary failover resource record sets\.

## Alias<a name="rrsets-values-failover-alias-alias"></a>

Select **Yes**\. 

**Note**  
When you create primary and secondary failover resource record sets, you can optionally create one failover and one failover *alias* resource record set that have the same values for **Name** and **Type**\. If you mix failover and failover alias resource record sets, either one can be the primary resource record set\. 

## Alias Target<a name="rrsets-values-failover-alias-alias-target"></a>

The value that you specify depends on the AWS resource that you're routing traffic to\.

**CloudFront Distributions**  
You can't create alias resource record sets for CloudFront distributions in a private hosted zone\.
For CloudFront distributions, do one of the following:  

+ **If you used the same account to create your Amazon Route 53 hosted zone and your CloudFront distribution** – Choose **Alias Target** and choose a distribution from the list\. If you have a lot of distributions, you can type the first few characters of the domain name for your distribution to filter the list\.

  If your distribution doesn't appear in the list, note the following:

  + The name of this resource record set must match an alternate domain name in your distribution\.

  + If you just added an alternate domain name to your distribution, it may take 15 minutes for your changes to propagate to all CloudFront edge locations\. Until changes have propagated, Amazon Route 53 can't know about the new alternate domain name\.

+ **If you used different accounts to create your Amazon Route 53 hosted zone and your distribution** – Enter the CloudFront domain name for the distribution, such as **d111111abcdef8\.cloudfront\.net**\.

  If you used one AWS account to create the current hosted zone and a different account to create a distribution, the distribution will not appear in the **Alias Targets** list\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your distributions, the **Alias Targets** list shows **No Targets Available** under **CloudFront Distributions**\.
Do not route queries to a CloudFront distribution that has not propagated to all edge locations, or your users won't be able to access the applicable content\. 
Your CloudFront distribution must include an alternate domain name that matches the name of the resource record set\. For example, if the name of the resource record set is **acme\.example\.com**, your CloudFront distribution must include **acme\.example\.com** as one of the alternate domain names\. For more information, see [Using Alternate Domain Names \(CNAMEs\)](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) in the *Amazon CloudFront Developer Guide*\.  
If IPv6 is enabled for the distribution, create two resource record sets, one with a value of **A — IPv4 address** for **Type**, and one with a value of **AAAA — IPv6 address**\.

**Elastic Beanstalk environments that have regionalized subdomains**  
For Elastic Beanstalk environments that have regionalized subdomains, do one of the following:  

+ **If you used the same account to create your Amazon Route 53 hosted zone and your Elastic Beanstalk environment** – Choose **Alias Target**, and then choose an environment from the list\. If you have a lot of environments, you can type the first few characters of the CNAME attribute for the environment to filter the list\.

+ **If you used different accounts to create your Amazon Route 53 hosted zone and your Elastic Beanstalk environment** – Enter the CNAME attribute for the Elastic Beanstalk environment\.

**ELB Load Balancers**  
For ELB load balancers, do one of the following:  

+ **If you used the same account to create your Amazon Route 53 hosted zone and your load balancer** – Choose **Alias Target** and choose a load balancer from the list\. If you have a lot of load balancers, you can type the first few characters of the DNS name to filter the list\.

+ **If you used different accounts to create your Amazon Route 53 hosted zone and your load balancer** – Enter the value that you got in the procedure [Getting the DNS Name for an ELB Load Balancer](resource-record-sets-creating.md#resource-record-sets-elb-dns-name-procedure)\.

  If you used one AWS account to create the current hosted zone and a different account to create a load balancer, the load balancer will not appear in the **Alias Targets** list\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your load balancers, the **Alias Targets** list shows **No Targets Available** under **Elastic Load Balancers**\.
In either case, the console prepends **dualstack\.** to the DNS name\. When a client, such as a web browser, requests the IP address for your domain name \(example\.com\) or subdomain name \(www\.example\.com\), the client can request an IPv4 address \(an A record\), an IPv6 address \(a AAAA record\), or both IPv4 and IPv6 addresses \(in separate requests\)\. The **dualstack\.** designation allows Amazon Route 53 to respond with the appropriate IP address for your load balancer based on which IP address format the client requested\.

**Amazon S3 Buckets**  
For Amazon S3 buckets that are configured as website endpoints, do one of the following:  

+ **If you used the same account to create your Amazon Route 53 hosted zone and your Amazon S3 bucket** – Choose **Alias Target** and choose a bucket from the list\. If you have a lot of buckets, you can type the first few characters of the DNS name to filter the list\.

  The value of **Alias Target** changes to the Amazon S3 website endpoint for your bucket\.

+ **If you used different accounts to create your Amazon Route 53 hosted zone and your Amazon S3 bucket** – Type the name of the region that you created your S3 bucket in\. Use the value that appears in the **Website Endpoint** column in the [Amazon Simple Storage Service Website Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html#s3_website_region_endpoints) table in the [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html) chapter of the *Amazon Web Services General Reference*\.

  If you used AWS accounts other than the current account to create your Amazon S3 buckets, the bucket won't appear in the **Alias Targets** list\.
You must configure the bucket for website hosting\. For more information, see [Configure a Bucket for Website Hosting](http://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\.  
The name of the resource record set must match the name of your Amazon S3 bucket\. For example, if the name of your Amazon S3 bucket is **acme\.example\.com**, the name of this resource record set must also be **acme\.example\.com**\.  
In a group of weighted alias, latency alias, failover alias, or geolocation alias resource record sets, you can create only one resource record set that routes queries to an Amazon S3 bucket because the name of the resource record set must match the name of the bucket and bucket names must be globally unique\.

**Resource Record Sets in this Hosted Zone**  
For resource record sets in this hosted zone, choose **Alias Target** and choose the applicable resource record set\. If you have a lot of resource record sets, you can type the first few characters of the name to filter the list\.  
If the hosted zone contains only the default NS and SOA resource record sets, the **Alias Targets** list shows **No Targets Available**\.

## Alias Hosted Zone ID<a name="rrsets-values-failover-alias-hosted-zone-id"></a>

This value appears automatically based on the value that you selected or entered for **Alias Target**\.

## Routing Policy<a name="rrsets-values-failover-alias-routing-policy"></a>

Select **Failover**\. 

## Failover Record Type<a name="rrsets-values-failover-alias-failover-record-type"></a>

Choose the applicable value for this resource record set\. For failover to function correctly, you must create one primary and one secondary failover resource record set\.

You can't create non\-failover resource record sets that have the same values for **Name** and **Type** as failover resource record sets\.

## Set ID<a name="rrsets-values-failover-alias-set-id"></a>

Enter a value that uniquely identifies the primary and secondary resource record sets\. 

## Evaluate Target Health<a name="rrsets-values-failover-alias-evaluate-target-health"></a>

Select **Yes** if you want Amazon Route 53 to determine whether to respond to DNS queries using this resource record set by checking the health of the resource specified by **Alias Target**\. 

Note the following:

+ **CloudFront distributions** – You cannot set **Evaluate Target Health** to **Yes** when the alias target is a CloudFront distribution\.

+ **Elastic Beanstalk environments that have regionalized endpoints** – If you specify an Elastic Beanstalk environment in **Alias Target** and the environment contains an ELB load balancer, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. \(An environment automatically contains an ELB load balancer if it includes more than one Amazon EC2 instance\.\) If you set **Evaluate Target Health** to **Yes** and either no Amazon EC2 instances are healthy or the load balancer itself is unhealthy, Amazon Route 53 routes queries to other available resources that are healthy, if any\. 

  If the environment contains a single Amazon EC2 instance, there are no special requirements\.

+ **ELB load balancers** – If you specify an ELB load balancer in **Alias Target**, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. If you set **Evaluate Target Health** to **Yes** and either no Amazon EC2 instances are healthy or the load balancer itself is unhealthy, Amazon Route 53 routes queries to other resources\.

  When you create a load balancer, you configure settings for Elastic Load Balancing health checks; they're not Amazon Route 53 health checks, but they perform a similar function\. Do not create Amazon Route 53 health checks for the Amazon EC2 instances that you register with an ELB load balancer\.

  For more information, see [How Health Checks Work in Complex Amazon Route 53 Configurations](dns-failover-complex-configs.md)\.

+ **S3 buckets** – There are no special requirements for setting **Evaluate Target Health** to **Yes** when the alias target is an S3 bucket\.

+ **Other resource record sets** – If the AWS resource that you specify in **Alias Target** is a resource record set or a group of resource record sets \(for example, a group of weighted resource record sets\) but is not another alias resource record set, we recommend that you associate a health check with all of the resource record sets in the alias target\. For more information, see [What Happens When You Omit Health Checks?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-omitting)\.

We recommend that you set **Evaluate Target Health** to **Yes** only when you have enough idle capacity to handle the failure of one or more endpoints\.

## Associate with Health Check/Health Check to Associate<a name="rrsets-values-failover-alias-associate-with-health-check"></a>

Select **Yes** if you want Amazon Route 53 to check the health of a specified endpoint and to respond to DNS queries using this resource record set only when the endpoint is healthy\. Then select the health check that you want Amazon Route 53 to perform for this resource record set\. 

Amazon Route 53 doesn't check the health of the endpoint specified in the resource record set, for example, the endpoint specified by the IP address in the **Value** field\. When you select a health check for a resource record set, Amazon Route 53 checks the health of the endpoint that you specified in the health check\. For information about how Amazon Route 53 determines whether an endpoint is healthy, see [How Amazon Route 53 Determines Whether an Endpoint Is Healthy](dns-failover-determining-health-of-endpoints.md)\.

Associating a health check with a resource record set is useful only when Amazon Route 53 is choosing between two or more resource record sets to respond to a DNS query, and you want Amazon Route 53 to base the choice in part on the status of a health check\. Use health checks only in the following configurations:

+ You're checking the health of all of the resource record sets in a group of failover, geolocation, latency, multivalue, or weighted resource record sets, and you specify health check IDs for all the resource record sets\. If the health check for a resource record set specifies an endpoint that is not healthy, Amazon Route 53 stops responding to queries using the value for that resource record set\.

+ You select **Yes** for **Evaluate Target Health** for an alias resource record set or the resource record sets in a group of failover alias, geolocation alias, latency alias, or weighted alias resource record set\. If the alias resource record sets reference non\-alias resource record sets in the same hosted zone, you must also specify health checks for the referenced resource record sets\. 

For geolocation resource record sets, if an endpoint is unhealthy, Amazon Route 53 looks for a resource record set for the larger, associated geographic region\. For example, suppose you have resource record sets for a state in the United States, for the United States, for North America, and for all locations \(**Location** is **Default**\)\. If the endpoint for the state resource record set is unhealthy, Amazon Route 53 checks the resource record sets for the United States, for North America, and for all locations, in that order, until it finds a resource record set that has a healthy endpoint\.

If your health checks specify the endpoint only by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain Name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the resource record sets \(example\.com\)\.

**Important**  
In this configuration, if you create a health check for which the value of **Domain Name** matches the name of the resource record sets and then associate the health check with those resource record sets, health check results will be unpredictable\.

For more information about checking the health of endpoints, see [Creating Amazon Route 53 Health Checks and Configuring DNS Failover](dns-failover.md)\.