# Values for Weighted Alias Records<a name="resource-record-sets-values-weighted-alias"></a>

When you create weighted alias records, you specify the following values:


+ [Name](#rrsets-values-weighted-alias-name)
+ [Type](#rrsets-values-weighted-alias-type)
+ [Alias](#rrsets-values-weighted-alias-alias)
+ [Alias Target](#rrsets-values-weighted-alias-alias-target)
+ [Alias Hosted Zone ID](#rrsets-values-weighted-alias-hosted-zone-id)
+ [Routing Policy](#rrsets-values-weighted-alias-routing-policy)
+ [Weight](#rrsets-values-weighted-alias-weight)
+ [Set ID](#rrsets-values-weighted-alias-set-identifier)
+ [Evaluate Target Health](#rrsets-values-weighted-alias-evaluate-target-health)
+ [Associate with Health Check/Health Check to Associate](#rrsets-values-weighted-alias-associate-with-health-check)

## Name<a name="rrsets-values-weighted-alias-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

Enter the same name for all of the records in the group of weighted records\. 

**CNAME records**  
If you're creating a record that has a value of **CNAME** for **Type**, the name of the record can't be the same as the name of the hosted zone\.

**Aliases to CloudFront distributions and Amazon S3 buckets**  
The value that you specify depends in part on the AWS resource that you're routing traffic to:  

+ **CloudFront distribution** – Your distribution must include an alternate domain name that matches the name of the record\. For example, if the name of the record is **acme\.example\.com**, your CloudFront distribution must include **acme\.example\.com** as one of the alternate domain names\. For more information, see [Using Alternate Domain Names \(CNAMEs\)](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) in the *Amazon CloudFront Developer Guide*\.

+ **Amazon S3 bucket** – The name of the record must match the name of your Amazon S3 bucket\. For example, if the name of your bucket is **acme\.example\.com**, the name of this record must also be **acme\.example\.com**\.

  In addition, you must configure the bucket for website hosting\. For more information, see [Configure a Bucket for Website Hosting](http://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\.

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an Asterisk \(\*\) in the Names of Hosted Zones and Records](DomainNameFormat.md#domain-name-format-asterisk)\.

## Type<a name="rrsets-values-weighted-alias-type"></a>

The DNS record type\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

Select the applicable value based on the AWS resource that you're routing traffic to:

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

Select the same value for all of the records in the group of weighted records\.

## Alias<a name="rrsets-values-weighted-alias-alias"></a>

Select **Yes**\. 

## Alias Target<a name="rrsets-values-weighted-alias-alias-target"></a>

The value that you specify depends on the AWS resource that you're routing traffic to\.

**CloudFront Distributions**  
For CloudFront distributions, do one of the following:  

+ **If you used the same account to create your Route 53 hosted zone and your CloudFront distribution** – Choose **Alias Target** and choose a distribution from the list\. If you have a lot of distributions, you can type the first few characters of the domain name for your distribution to filter the list\.

  If your distribution doesn't appear in the list, note the following:

  + The name of this record must match an alternate domain name in your distribution\.

  + If you just added an alternate domain name to your distribution, it may take 15 minutes for your changes to propagate to all CloudFront edge locations\. Until changes have propagated, Route 53 can't know about the new alternate domain name\.

+ **If you used different accounts to create your Route 53 hosted zone and your distribution** – Enter the CloudFront domain name for the distribution, such as **d111111abcdef8\.cloudfront\.net**\.

  If you used one AWS account to create the current hosted zone and a different account to create a distribution, the distribution will not appear in the **Alias Targets** list\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your distributions, the **Alias Targets** list shows **No Targets Available** under **CloudFront Distributions**\.
Do not route queries to a CloudFront distribution that has not propagated to all edge locations, or your users won't be able to access the applicable content\. 
Your CloudFront distribution must include an alternate domain name that matches the name of the record\. For example, if the name of the record is **acme\.example\.com**, your CloudFront distribution must include **acme\.example\.com** as one of the alternate domain names\. For more information, see [Using Alternate Domain Names \(CNAMEs\)](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) in the *Amazon CloudFront Developer Guide*\.  
If IPv6 is enabled for the distribution, create two records, one with a value of **A — IPv4 address** for **Type**, and one with a value of **AAAA — IPv6 address**\.

**Elastic Beanstalk environments that have regionalized subdomains**  
If the domain name for your Elastic Beanstalk environment includes the region that you deployed the environment in, you can create an alias record that routes traffic to the environment\. For example, the domain name `my-environment.us-west-2.elasticbeanstalk.com` is a regionalized domain name\.  
For environments that were created before early 2016, the domain name doesn't include the region\. To route traffic to these environments, you must create a CNAME record instead of an alias record\. Note that you can't create a CNAME record for the root domain name\. For example, if your domain name is example\.com, you can create a record that routes traffic for acme\.example\.com to your Elastic Beanstalk environment, but you can't create a record that routes traffic for example\.com to your Elastic Beanstalk environment\.
For Elastic Beanstalk environments that have regionalized subdomains, do one of the following:  

+ **If you used the same account to create your Route 53 hosted zone and your Elastic Beanstalk environment** – Choose **Alias Target**, and then choose an environment from the list\. If you have a lot of environments, you can type the first few characters of the CNAME attribute for the environment to filter the list\.

+ **If you used different accounts to create your Route 53 hosted zone and your Elastic Beanstalk environment** – Enter the CNAME attribute for the Elastic Beanstalk environment\.

**ELB Load Balancers**  
For ELB load balancers, do one of the following:  

+ **If you used the same account to create your Route 53 hosted zone and your load balancer** – Choose **Alias Target** and choose a load balancer from the list\. If you have a lot of load balancers, you can type the first few characters of the DNS name to filter the list\.

+ **If you used different accounts to create your Route 53 hosted zone and your load balancer** – Enter the value that you got in the procedure [Getting the DNS Name for an ELB Load Balancer](resource-record-sets-creating.md#resource-record-sets-elb-dns-name-procedure)\.

  If you used one AWS account to create the current hosted zone and a different account to create a load balancer, the load balancer will not appear in the **Alias Targets** list\.

  If you used one account to create the current hosted zone and one or more different accounts to create all of your load balancers, the **Alias Targets** list shows **No Targets Available** under **Elastic Load Balancers**\.
In either case, the console prepends **dualstack\.** to the DNS name\. When a client, such as a web browser, requests the IP address for your domain name \(example\.com\) or subdomain name \(www\.example\.com\), the client can request an IPv4 address \(an A record\), an IPv6 address \(a AAAA record\), or both IPv4 and IPv6 addresses \(in separate requests\)\. The **dualstack\.** designation allows Route 53 to respond with the appropriate IP address for your load balancer based on which IP address format the client requested\.

**Amazon S3 Buckets**  
For Amazon S3 buckets that are configured as website endpoints, do one of the following:  

+ **If you used the same account to create your Route 53 hosted zone and your Amazon S3 bucket** – Choose **Alias Target** and choose a bucket from the list\. If you have a lot of buckets, you can type the first few characters of the DNS name to filter the list\.

  The value of **Alias Target** changes to the Amazon S3 website endpoint for your bucket\.

+ **If you used different accounts to create your Route 53 hosted zone and your Amazon S3 bucket** – Type the name of the region that you created your S3 bucket in\. Use the value that appears in the **Website Endpoint** column in the [Amazon Simple Storage Service Website Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html#s3_website_region_endpoints) table in the [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html) chapter of the *Amazon Web Services General Reference*\.

  If you used AWS accounts other than the current account to create your Amazon S3 buckets, the bucket won't appear in the **Alias Targets** list\.
You must configure the bucket for website hosting\. For more information, see [Configure a Bucket for Website Hosting](http://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html) in the *Amazon Simple Storage Service Developer Guide*\.  
The name of the record must match the name of your Amazon S3 bucket\. For example, if the name of your Amazon S3 bucket is **acme\.example\.com**, the name of this record must also be **acme\.example\.com**\.  
In a group of weighted alias, latency alias, failover alias, or geolocation alias records, you can create only one record that routes queries to an Amazon S3 bucket because the name of the record must match the name of the bucket and bucket names must be globally unique\.

**Records in this Hosted Zone**  
For records in this hosted zone, choose **Alias Target** and choose the applicable record\. If you have a lot of records, you can type the first few characters of the name to filter the list\.  
If the hosted zone contains only the default NS and SOA records, the **Alias Targets** list shows **No Targets Available**\.

## Alias Hosted Zone ID<a name="rrsets-values-weighted-alias-hosted-zone-id"></a>

This value appears automatically based on the value that you selected or entered for **Alias Target**\.

## Routing Policy<a name="rrsets-values-weighted-alias-routing-policy"></a>

Select **Weighted**\.

## Weight<a name="rrsets-values-weighted-alias-weight"></a>

A value that determines the proportion of DNS queries that Route 53 responds to using the current record\. Route 53 calculates the sum of the weights for the records that have the same combination of DNS name and type\. Route 53 then responds to queries based on the ratio of a resource's weight to the total\. 

You can't create non\-weighted records that have the same values for **Name** and **Type** as weighted records\.

Enter an integer between 0 and 255\. To disable routing to a resource, set **Weight** to 0\. If you set **Weight** to 0 for all of the records in the group, traffic is routed to all resources with equal probability\. This ensures that you don't accidentally disable routing for a group of weighted records\.

The effect of setting **Weight** to 0 is different when you associate health checks with weighted records\. For more information, see [Configuring Active\-Active or Active\-Passive Failover by Using Amazon Route 53 Weighted and Weighted Alias Records](dns-failover-configuring-options.md#dns-failover-weighted-rrsets)\.

## Set ID<a name="rrsets-values-weighted-alias-set-identifier"></a>

Enter a value that uniquely identifies this record in the group of weighted records\.

## Evaluate Target Health<a name="rrsets-values-weighted-alias-evaluate-target-health"></a>

Select **Yes** if you want Route 53 to determine whether to respond to DNS queries using this record by checking the health of the resource specified by **Alias Target**\. 

Note the following:

**CloudFront distributions**  
You can't set **Evaluate Target Health** to **Yes** when the alias target is a CloudFront distribution\.

**Elastic Beanstalk environments that have regionalized subdomains**  
If you specify an Elastic Beanstalk environment in **Alias Target** and the environment contains an ELB load balancer, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. \(An environment automatically contains an ELB load balancer if it includes more than one Amazon EC2 instance\.\) If you set **Evaluate Target Health** to **Yes** and either no Amazon EC2 instances are healthy or the load balancer itself is unhealthy, Route 53 routes queries to other available resources that are healthy, if any\.   
If the environment contains a single Amazon EC2 instance, there are no special requirements\.

**ELB load balancers**  
Health checking behavior depends on the type of load balancer:  

+ **Classic Load Balancers** – If you specify an ELB Classic Load Balancer in **Alias Target**, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. If you set **Evaluate Target Health** to **Yes** and either no EC2 instances are healthy or the load balancer itself is unhealthy, Route 53 routes queries to other resources\.

+ **Application and Network Load Balancers** – If you specify an ELB Application or Network Load Balancer and you set **Evaluate Target Health** to **Yes**, Route 53 routes queries to the load balancer based on the health of the target groups that are associated with the load balancer:

  + For an Application or Network Load Balancer to be considered healthy, every target group that contains targets must contain at least one healthy target\. If any target group contains only unhealthy targets, the load balancer is considered unhealthy, and Route 53 routes queries to other resources\.

  + A target group that has no registered targets is considered healthy\.
When you create a load balancer, you configure settings for Elastic Load Balancing health checks; they're not Route 53 health checks, but they perform a similar function\. Do not create Route 53 health checks for the EC2 instances that you register with an ELB load balancer\. 

**S3 buckets**  
There are no special requirements for setting **Evaluate Target Health** to **Yes** when the alias target is an S3 bucket\.

**Other records in the same hosted zone**  
If the AWS resource that you specify in **Alias Target** is a record or a group of records \(for example, a group of weighted records\) but is not another alias record, we recommend that you associate a health check with all of the records in the alias target\. For more information, see [What Happens When You Omit Health Checks?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-omitting)\.

## Associate with Health Check/Health Check to Associate<a name="rrsets-values-weighted-alias-associate-with-health-check"></a>

Select **Yes** if you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy\. Then select the health check that you want Route 53 to perform for this record\. 

Route 53 doesn't check the health of the endpoint specified in the record, for example, the endpoint specified by the IP address in the **Value** field\. When you select a health check for a record, Route 53 checks the health of the endpoint that you specified in the health check\. For information about how Route 53 determines whether an endpoint is healthy, see [How Amazon Route 53 Determines Whether an Endpoint Is Healthy](dns-failover-determining-health-of-endpoints.md)\.

Associating a health check with a record is useful only when Route 53 is choosing between two or more records to respond to a DNS query, and you want Route 53 to base the choice in part on the status of a health check\. Use health checks only in the following configurations:

+ You're checking the health of all of the records in a group of failover, geolocation, latency, multivalue, or weighted records, and you specify health check IDs for all the records\. If the health check for a record specifies an endpoint that is not healthy, Route 53 stops responding to queries using the value for that record\.

+ You select **Yes** for **Evaluate Target Health** for an alias record or the records in a group of failover alias, geolocation alias, latency alias, or weighted alias record\. If the alias records reference non\-alias records in the same hosted zone, you must also specify health checks for the referenced records\. 

For geolocation records, if an endpoint is unhealthy, Route 53 looks for a record for the larger, associated geographic region\. For example, suppose you have records for a state in the United States, for the United States, for North America, and for all locations \(**Location** is **Default**\)\. If the endpoint for the state record is unhealthy, Route 53 checks the records for the United States, for North America, and for all locations, in that order, until it finds a record that has a healthy endpoint\.

If your health checks specify the endpoint only by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain Name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the records \(example\.com\)\.

**Important**  
In this configuration, if you create a health check for which the value of **Domain Name** matches the name of the records and then associate the health check with those records, health check results will be unpredictable\.

For more information about checking the health of endpoints, see [Creating Amazon Route 53 Health Checks and Configuring DNS Failover](dns-failover.md)\.