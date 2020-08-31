# Document history<a name="History"></a>

The following entries describe important changes in each release of the Route 53 documentation\. For notification about updates to this documentation, you can subscribe to an RSS feed\. 

**Topics**
+ [2018 releases](#doc-history-2018)
+ [2017 releases](#doc-history-2017)
+ [2016 releases](#doc-history-2016)
+ [2015 releases](#doc-history-2015)
+ [2014 releases](#doc-history-2014)
+ [2013 releases](#doc-history-2013)
+ [2012 release](#doc-history-2012)
+ [2011 releases](#doc-history-2011)
+ [2010 release](#doc-history-2010)

## 2018 releases<a name="doc-history-2018"></a>

**December 20, 2018**  
You can create Route 53 alias records that route traffic to API Gateway APIs or to Amazon VPC interface endpoints\. For more information, see [Alias target](resource-record-sets-values-alias.md#rrsets-values-alias-alias-target)\.

**November 28, 2018**  
Route 53 Auto Naming \(also known as Service Discovery\) is now a separate service, AWS Cloud Map\. For more information, see the [AWS Cloud Map Developer Guide](https://docs.aws.amazon.com/cloud-map/latest/dg/)\.

**November 19, 2018**  
You can use Route 53 Resolver to configure DNS resolution between your VPC and your network over a Direct Connect or VPN connection\. \(Resolver is the new name for the recursive DNS service that is provided to all customers by default in Amazon Virtual Private Cloud \(Amazon VPC\)\.\) This lets you forward DNS queries from resolvers on your network to Route 53 Resolver\. Resolver also lets you forward queries for selected domain names \(example\.com\) and subdomain names \(api\.example\.com\) from a VPC to resolvers on your network\. For more information, see [Resolving DNS queries between VPCs and your network](resolver.md)\.

**November 7, 2018**  
When you're using Route 53 traffic flow and geoproximity routing, you can use an interactive map to visualize how your end users will be routed to your endpoints around the world\. For more information, see [Viewing a map that shows the effect of geoproximity settings](traffic-policies.md#traffic-flow-geoproximity-map)\.

**October 18, 2018**  
You can use the Route 53 console and API to temporarily disable a Route 53 health check\. This gives you an easy way to pause monitoring of an endpoint, such a web server, so that you can perform maintenance on it without triggering alarms or generating unnecessary logs or status messages\. For more information, see "Disabled" in [Values that you specify when you create or update health checks](health-checks-creating-values.md)\. The feature is available for all three types of Route 53 health checks: health checks that monitor an endpoint, health checks that monitor other health checks, and health checks that monitor a CloudWatch alarm\.

**March 13, 2018**  
If you're using auto naming, you can now use a third\-party health checker to evaluate the health of your resources\. This is useful when a resource isn't available over the internet, for example, because the instance is in an Amazon VPC\. For more information, see [HealthCheckCustomConfig](https://docs.aws.amazon.com/cloud-map/latest/api/API_HealthCheckCustomConfig.html) in the *Amazon Route 53 API Reference*\.

**March 9, 2018**  
IAM now includes managed policies for auto naming\. For more information, see [AWS managed \(predefined\) policies for Route 53](access-control-managing-permissions.md#access-policy-examples-aws-managed)\.

**February 6, 2018**  
You can now configure auto naming to create alias records that route traffic to ELB load balancers or to create CNAME records\. For more information, see [Attributes](https://docs.aws.amazon.com/cloud-map/latest/api/API_RegisterInstance.html#cloudmap-RegisterInstance-request-Attributes) in the documentation for the [RegisterInstance](https://docs.aws.amazon.com/Route53/latest/APIReference/API_autonaming_RegisterInstance.html) API in the *Amazon Route 53 API Reference*\.

## 2017 releases<a name="doc-history-2017"></a>

**December 5, 2017**  
You can now use the Route 53 autonaming API to provision instances for microservices\. Autonaming lets you automatically create DNS records and, optionally, health checks based on a template that you define\. For more information, see [What is AWS Cloud Map?](https://docs.aws.amazon.com/cloud-map/latest/dg/) in the *AWS Cloud Map Developer Guide*\.

**November 16, 2017**  
You can now programmatically get both the current quotas on Route 53 resources such as hosted zones and health checks, and the number of each resource that you're currently using\. For more information, see [GetAccountLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetAccountLimit.html), [GetHostedZoneLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneLimit.html), and [GetReusableDelegationSetLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetReusableDelegationSetLimit.html) in the *Amazon Route 53 API Reference*\.

**October 3, 2017**  
Route 53 is now a HIPAA eligible service\. For more information, see [Compliance validation for Amazon Route 53](route-53-compliance.md)\.

**September 29, 2017**  
You can now programmatically check whether a domain can be transferred to Route 53\. For more information, see [CheckDomainTransferability](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_CheckDomainTransferability.html) in the *Amazon Route 53 API Reference*\. 

**September 11, 2017**  
You can now create Route 53 alias records that route internet traffic to Elastic Load Balancing Network Load Balancers\. For more information about alias records, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**September 7, 2017**  
If you're using Route 53 as your public, authoritative DNS service, you can now log DNS queries that Route 53 receives\. For more information, see [Public DNS query logging](query-logs.md)\.

**September 1, 2017**  
If you're using Route 53 traffic flow, you can now use geoproximity routing, which lets you route traffic based on the physical distance between your users and your resources\. You can also route more or less traffic to each resource by specifying a positive or negative bias\. For more information, see [Geoproximity routing \(traffic flow only\)](routing-policy.md#routing-policy-geoproximity)\.

**August 21, 2017**  
You can now use Route 53 to create Certification Authority Authorization \(CAA\) records, which let you specify the certificate authorities that can issue certificates for your domains and subdomains\. For more information, see [CAA record type](ResourceRecordTypes.md#CAAFormat)\.

**August 18, 2017**  
You can now transfer large numbers of domains to Route 53 using the Route 53 console\. For more information, see [Transferring registration for a domain to Amazon Route 53](domain-transfer-to-route-53.md)\.

**August 4, 2017**  
When you register a domain, the registries for some top\-level domains \(TLDs\) require you to verify that you specified a valid email address for the registrant contact\. You can now send the verification email and get confirmation that you successfully verified the email address during the domain registration process\. For more information, see [Registering a new domain](domain-register.md)\.

**June 21, 2017**  
If you want to route traffic approximately randomly to multiple resources, such as web servers, you can now create one multivalue answer record for each resource and, optionally, associate a Route 53 health check with each record\. Route 53 responds to DNS queries with up to eight healthy records in response to each DNS query, and gives different answers to different DNS resolvers\. For more information, see [Multivalue answer routing](routing-policy.md#routing-policy-multivalue)\.

**April 10, 2017**  
When you use the Route 53 console to transfer a domain registration to Route 53, you can now choose one of the following options for associating the name servers for the DNS service for the domain with the transferred domain registration:  
+ Use the name servers for a Route 53 hosted zone that you choose
+ Use the name servers for the current DNS service for the domain
+ Use name servers that you specify
Route 53 automatically associates these name servers with the transferred domain registration\.

## 2016 releases<a name="doc-history-2016"></a>

**November 21, 2016**  
You can now create health checks that use IPv6 addresses to check the health of endpoints\. For more information, see [Creating and updating health checks](health-checks-creating.md)\.

**November 15, 2016**  
You can now use a Route 53 API action to associate an Amazon VPC that you created with one account with a private hosted zone that you created with another account\. For more information, see [Associating an Amazon VPC and a private hosted zone that you created with different AWS accounts](hosted-zone-private-associate-vpcs-different-accounts.md)\.

**August 30, 2016**  
With this release, Route 53 adds the following new features:  
+ **Name Authority Pointer \(NAPTR\) records** – You can now create NAPTR records, which are used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For example, one common use is to convert phone numbers into SIP URIs\. For more information, see [NAPTR record type](ResourceRecordTypes.md#NAPTRFormat)\.
+ **DNS query test tool** – You can now simulate DNS queries for a record and see the value that Route 53 returns\. For geolocation and latency records, you can also simulate requests from a particular DNS resolver and/or client IP address to find out what response Route 53 would return to a client with that resolver and/or IP address\. For more information, see [Checking DNS responses from Route 53](dns-test.md)\.

**August 11, 2016**  
With this release, you can create alias records that route traffic to ELB Application Load Balancers\. The process is the same as for Classic Load Balancers\. For more information, see [Alias target](resource-record-sets-values-alias.md#rrsets-values-alias-alias-target)\.

**August 9, 2016**  
With this release, Route 53 adds support for DNSSEC for domain registration\. DNSSEC lets you protect your domain from DNS spoofing attacks, which are also known as man\-in\-the\-middle attacks\. For more information, see [Configuring DNSSEC for a domain](domain-configure-dnssec.md)\.

**July 7, 2016**  
You can now manually extend the registration for a domain and register a domain with an initial registration period longer than the minimum registration period specified by the registry\. For more information, see [Extending the registration period for a domain](domain-extend.md)\.

**July 6, 2016**  
If you're an AISPL customer with a contact address in India, you can now use Route 53 to register domains\. For more information, see [Managing an Account in India](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-account-payment-aispl.html)\.

**May 26, 2016**  
With this release, Route 53 adds the following new features:  
+ **Domain billing report** – You can now download a report that lists all domain registration charges, by domain, for a specified time period\. The report includes all domain registration operations for which there is a fee, including registering domains, transferring domains to Route 53, renewing domain registration, and \(for some TLDs\), changing the owner of a domain\. For more information, see the following documentation:
  + **Route 53 console** – See [Downloading a domain billing report](domain-billing-report.md)
  + **Route 53 API** – See [ViewBilling](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ViewBilling.html) in the *Amazon Route 53 API Reference*\.
+ **New TLDs** – You can now register domains that have the following TLDs: \.college, \.consulting, \.host, \.name, \.online, \.republican, \.rocks, \.sucks, \.trade, \.website, and \.uk\. For more information, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.
+ **New APIs for domain registration** – For operations that require confirmation that the email address for the registrant contact is valid, such as registering a new domain, you can now programmatically determine whether the registrant contact has clicked the link in the confirmation email and, if not, whether the link is still valid\. You can also programmatically request that we send another confirmation email\. For more information, see the following documentation in the *Amazon Route 53 API Reference*:
  + [GetContactReachabilityStatus](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetContactReachabilityStatus.html)
  + [ResendContactReachabilityEmail](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ResendContactReachabilityEmail.html)

**April 5, 2016**  
With this release, Route 53 adds the following new features:  
+ **Health checks based on CloudWatch metrics** – You can now create health checks that are based on the alarm state of any CloudWatch metric\. This is useful for checking the health of endpoints that can't be reached by a standard Route 53 health check, such as instances within an Amazon Virtual Private Cloud \(VPC\) that have only private IP addresses\. For more information, see the following documentation:
  + **Route 53 console** – See [Monitoring a CloudWatch alarm](health-checks-creating-values.md#health-checks-creating-values-cloudwatch) in the "Values that You Specify When You Create or Update Health Checks" topic\. 
  + **Route 53 API** – See [CreateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html) and [UpdateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHealthCheck.html) in the *Amazon Route 53 API Reference*\.
+ **Configurable health check locations** – You can now choose the Route 53 health checking regions that check the health of your resources, which reduces the load on the endpoint from health checks\. This is useful if your customers are concentrated in one or a few geographic regions\. For more information, see the following documentation:
  + **Route 53 console** – See [Health checker regions](health-checks-creating-values.md#health-checks-creating-values-health-checker-regions) in the "Values that You Specify When You Create or Update Health Checks" topic\. 
  + **Route 53 API** – See the `Regions` element for [CreateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html) and [UpdateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHealthCheck.html) in the *Amazon Route 53 API Reference*\.
+ **Failover in private hosted zones** – You can now create failover and failover alias records in a private hosted zone\. When you combine this feature with metric\-based health checks, you can configure DNS failover even for endpoints that have only private IP addresses and can't be reached by using standard Route 53 health checks\. For more information, see the following documentation:
  + **Route 53 console** – See [Configuring failover in a private hosted zone](dns-failover-private-hosted-zones.md)\.
  + **Route 53 API** – See [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.
+ **Alias records in private hosted zones** – In the past, you could create alias records that route DNS queries only to other Route 53 records in the same hosted zone\. With this release, you can also create alias records that route DNS queries to Elastic Beanstalk environments that have regionalized subdomains, Elastic Load Balancing load balancers, and Amazon S3 buckets\. \(You still can't create alias records that route DNS queries to a CloudFront distribution\.\) For more information, see the following documentation:
  + **Route 53 console** – See [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.
  + **Route 53 API** – See [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

**February 23, 2016**  
When you create or update HTTPS health checks, you can now configure Route 53 to send the host name to the endpoint during TLS negotiation\. This allows the endpoint to respond to the HTTPS request with the applicable SSL/TLS certificate\. For more information, see the description for the [Enable SNI](health-checks-creating-values.md#health-checks-creating-values-enable-sni) field in the "Values that You Specify When You Create or Update Health Checks" topic\. For information about how to enable SNI when you use the API to create or update a health check, see [CreateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html) and [UpdateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHealthCheck.html) in the *Amazon Route 53 API Reference*\.

**January 27, 2016**  
You can now register domains for over 100 additional top\-level domains \(TLDs\) such as \.accountants, \.band, and \.city\. For a complete list of supported TLDs, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

**January 19, 2016**  
You can now create alias records that route traffic to Elastic Beanstalk environments\. For information about creating records by using the Route 53 console, see [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)\. For information about using the API to create records, see [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

## 2015 releases<a name="doc-history-2015"></a>

**December 3, 2015**  
The Route 53 console now includes a visual editor that lets you quickly create complex routing configurations that use a combination of Route 53 weighted, latency, failover, and geolocation routing policies\. You can then associate the configuration with one or more domain names \(such as example\.com\) or subdomain names \(such as www\.example\.com\), in the same hosted zone or in multiple hosted zones\. In addition, you can roll back the updates if the new configuration isn't performing as you expected it to\. The same functionality is available by using the Route 53 API, AWS SDKs, the AWS CLI, and AWS Tools for Windows PowerShell\. For information about using the visual editor, see [Using traffic flow to route DNS traffic](traffic-flow.md)\. For information about using the API to create traffic flow configurations, see the [Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/)\.

**October 19, 2015**  
With this release, Route 53 adds the following new features:  
+ **Domain registration for \.com and \.net domains by Amazon Registrar, Inc\.** – Amazon is now an ICANN\-accredited registrar for the \.com and \.net top\-level domains \(TLDs\) through Amazon Registrar, Inc\. When you use Route 53 to register a \.com or \.net domain, Amazon Registrar will be the registrar of record and will be listed as the "Sponsoring Registrar" in your Whois query results\. For information about using Route 53 to register domains, see [Registering domain names using Amazon Route 53](registrar.md)\.
+ **Privacy protection for \.com and \.net domains** – When you register a \.com or \.net domain with Route 53, all of your personal information, including first and last name, is now hidden\. First and last name are not hidden for other domains that you register with Route 53\. For more information about privacy protection, see [Enabling or disabling privacy protection for contact information for a domain](domain-privacy-protection.md)\.

**September 15, 2015**  
With this release, Route 53 adds the following new features:  
+ **Calculated health checks** – You can now create health checks whose status is determined by the health status of other health checks\. For more information, see [Creating and updating health checks](health-checks-creating.md)\. In addition, see [CreateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html) in the *Amazon Route 53 API Reference*\.
+ **Latency measurements for health checks** – You can now configure Route 53 to measure the latency between health checkers and your endpoint\. Latency data appears in Amazon CloudWatch graphs in the Route 53 console\. To enable latency measurements for new health checks, see the **Latency measurements** setting under [Advanced configuration \("Monitor an Endpoint" only\)](health-checks-creating-values.md#health-checks-creating-values-advanced) in the topic [Values that you specify when you create or update health checks](health-checks-creating-values.md)\. \(You can't enable latency measurements for existing health checks\.\) In addition, see **MeasureLatency** in the topic [CreateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html) in the *Amazon Route 53 API Reference*\.
+ **Updates to the health checks dashboard in the Route 53 console** – The dashboard for monitoring health checks has been improved in a variety of ways, including CloudWatch graphs for monitoring latency between Route 53 health checkers and your endpoints\. For more information, see [Monitoring health check status and getting notifications](health-checks-monitor-view-status.md)\.

**March 3, 2015**  
The *Amazon Route 53 Developer Guide* now explains how to configure white\-label name servers for Route 53 hosted zones\. For more information, see [Configuring white\-label name servers](white-label-name-servers.md)\.

**February 26, 2015**  
You can now use the Route 53 API to list the hosted zones that are associated with an AWS account in alphabetical order by name\. You can also get a count of the hosted zones that are associated with an account\. For more information, see [ListHostedZonesByName](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZonesByName.html) and [GetHostedZoneCount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneCount.html) in the *Amazon Route 53 API Reference*\.

**February 11, 2015**  
With this release, Route 53 adds the following new features:  
+ **Health Check Status** – The health checks page in the Route 53 console now includes a **Status** column that lets you view the overall status of all of your health checks\. For more information, see [Viewing health check status and the reason for health check failures](health-checks-view-status.md)\.
+ **Integration with AWS CloudTrail** – Route 53 now works with CloudTrail to capture information about every request that your AWS account \(including your IAM users\) sends to the Route 53 API\. Integrating Route 53 and CloudTrail lets you determine which requests were made to the Route 53 API, the source IP address from which each request was made, who made the request, when it was made, and more\. For more information, see [Logging Amazon Route 53 API calls with AWS CloudTrail](logging-using-cloudtrail.md)\.
+ **Quick Alarms for Health Checks** – When you create a health check by using the Route 53 console, you can now simultaneously create an Amazon CloudWatch alarm for the health check and specify who to notify when Route 53 considers the endpoint unhealthy for one minute\. For more information, see [Creating and updating health checks](health-checks-creating.md)\.
+ **Tagging for Hosted Zones and Domains** – You can now assign tags, which are commonly used for cost allocation, to Route 53 hosted zones and domains\. For more information, see [Tagging Amazon Route 53 resources](tagging-resources.md)\.

**February 5, 2015**  
You can now use the Route 53 console to update contact information for a domain\. For more information, see [Values that you specify when you register or transfer a domain](domain-register-values-specify.md)\.

**January 22, 2015**  
You can now specify internationalized domain names when you're registering a new domain name with Route 53\. \(Route 53 already supported internationalized domain names for hosted zones and records\.\) For more information, see [DNS domain name format](DomainNameFormat.md)\.

## 2014 releases<a name="doc-history-2014"></a>

**November 25, 2014**  
With this release, you can now edit the comment that you specified for a hosted zone when you created it\. In the console, you just click the pencil icon next to the **Comment** field and enter a new value\. For more information about changing the comment by using the Route 53 API, see [UpdateHostedZoneComment](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHostedZoneComment.html) in the *Amazon Route 53 API Reference*\.

**November 5, 2014**  
With this release, Route 53 adds the following new features:  
+ **Private DNS for VPCs created using the Amazon Virtual Private Cloud service** – You can now use Route 53 to manage your internal domain names for VPCs without exposing DNS data to the public internet\. For more information, see [Working with private hosted zones](hosted-zones-private.md)\.
+ **Health check failure reasons** – You can now see the current status of a selected health check, as well as details on why the health check last failed, as reported by each of the Route 53 health checkers\. The status includes the HTTP status code, and failure reasons include information about numerous types of failures, such as string matching failures and response timeouts\. For more information, see [Viewing health check status and the reason for health check failures](health-checks-view-status.md)\.
+ **Reusable delegation sets** – You can now apply the same set of four authoritative name servers, known collectively as a delegation set, to multiple hosted zones that correspond with different domain names\. This greatly simplifies the process of migrating DNS service to Route 53 and managing large numbers of hosted zones\. Using reusable delegation sets currently requires that you use the Route 53 API or an AWS SDK\. For more information, see the [Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/)\.
+ **Improved geolocation routing** – We further improved the accuracy of geolocation routing by adding support for the edns\-client\-subnet extension of EDNS0\. For more information, see [Geolocation routing](routing-policy.md#routing-policy-geo)\.
+ **Support for Signature v4** – You can now sign all Route 53 API requests using Signature version 4\. For more information, see [Signing Route 53 API Requests](https://docs.aws.amazon.com/Route53/latest/APIReference/requests-authentication.html) in the *Amazon Route 53 API Reference*\.

**July 31, 2014**  
With this release, you can now do the following:  
+ Register domain names using Route 53\. For more information, see [Registering domain names using Amazon Route 53](registrar.md)\.
+ Configure Route 53 to respond to DNS queries based on the geographic location that the queries originate from\. For more information, see [Geolocation routing](routing-policy.md#routing-policy-geo)\.

**July 2, 2014**  
With this release, you can now do the following:  
+ Edit most values in health checks\. For more information, see [Creating, updating, and deleting health checks](health-checks-creating-deleting.md)\.
+ Use the Route 53 API to get a list of the IP ranges that Route 53 health checkers use to check the health of your resources\. You can use these IP addresses to configure your router and firewall rules to allow health checkers to check the health of your resources\. For more information, see [GetCheckerIpRanges](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetCheckerIpRanges.html) in the *Amazon Route 53 API Reference*\.
+ Assign cost allocation tags to health checks, which also lets you assign a name to health checks\. For more information, see [Naming and tagging health checks](health-checks-tagging.md)\.
+ Use the Route 53 API to get the number of health checks that are associated with your AWS account\. For more information, see [GetHealthCheckCount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheckCount.html) in the *Amazon Route 53 API Reference*\.

**April 30, 2014**  
With this release, you can now create health checks and use a domain name instead of an IP address to specify the endpoint\. This is helpful when an endpoint's IP address either is not fixed or is served by multiple IPs, such as Amazon EC2 or Amazon RDS instances\. For more information, see [Creating and updating health checks](health-checks-creating.md)\.  
In addition, some information about using the Route 53 API that formerly appeared in the *Amazon Route 53 Developer Guide* has been moved\. Now all API documentation appears in the *Amazon Route 53 API Reference*\. 

**April 18, 2014**  
With this release, Route 53 passes a different value in the `Host` header when the health check **Port** value is **443** and the **Protocol** value is **HTTPS**\. During a health check, Route 53 now passes to the endpoint a `Host` header that contains the value of the **Host Name** field\. If you created the health check by using the `CreateHealthCheck` API action, this is the value of the `FullyQualifiedDomainName` element\.  
For more information, see [Creating, updating, and deleting health checks](health-checks-creating-deleting.md)\.

**April 9, 2014**  
With this release, you can now view what percentage of Route 53 health checkers are currently reporting that an endpoint is healthy\.  
In addition, behavior of the Health Check Status metric in Amazon CloudWatch now shows only zero \(if your endpoint was unhealthy during a given time period\) or one \(if the endpoint was healthy for that time period\)\. The metric no longer shows values between 0 and 1 reflecting the portion of Route 53 health checks that are reporting the endpoint as healthy\.  
For more information, see [Monitoring health checks using CloudWatch](monitoring-health-checks.md)\.

**February 18, 2014**  
With this release, Route 53 adds the following features:  
+ **Health check failover threshold:** You can now specify how many consecutive health checks an endpoint must fail before Route 53 considers the endpoint unhealthy, between 1 and 10 consecutive checks\. An unhealthy endpoint must pass the same number of checks to be considered healthy\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.
+ **Health check request interval:** You can now specify how frequently Route 53 sends requests to an endpoint to determine whether the endpoint is healthy\. Valid settings are 10 seconds and 30 seconds\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

**January 30, 2014**  
With this release, Route 53 adds the following features:  
+ **HTTP and HTTPS string\-match health checks:** Route 53 now supports health checks that determine the health of an endpoint based on the appearance of a specified string in the response body\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.
+ **HTTPS health checks:** Route 53 now supports health checks for secure, SSL\-only websites\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.
+ **`UPSERT` for the `ChangeResourceRecordSets` API Action:** When creating or changing records using the `ChangeResourceRecordSets` API action, you can now use the `UPSERT` action either to create a new record if none exists with a given name and type, or to update an existing record\. For more information, see [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

**January 7, 2014**  
With this release, Route 53 adds support for health checks that determine the health of an endpoint based on whether a specified string appears in the response body\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

## 2013 releases<a name="doc-history-2013"></a>

**August 14, 2013**  
With this release, Route 53 adds support for creating records by importing a BIND\-formatted zone file\. For more information, see [Creating records by importing a zone file](resource-record-sets-creating-import.md)\.  
In addition, CloudWatch metrics for Route 53 health checks have been integrated into the Route 53 console and streamlined\. For more information, see [Monitoring health checks using CloudWatch](monitoring-health-checks.md)\.

**June 26, 2013**  
With this release, Route 53 adds support for integrating health checks with CloudWatch metrics so you can do the following:  
+ Verify that a health check is properly configured\.
+ Review the health of a health check endpoint over a specified period of time\.
+ Configure CloudWatch to send an Amazon Simple Notification Service \(Amazon SNS\) alert when all Route 53 health checkers consider your specified endpoint to be unhealthy\. 
For more information, see [Monitoring health checks using CloudWatch](monitoring-health-checks.md)\.

**June 11, 2013**  
With this release, Route 53 adds support for creating alias records that route DNS queries to alternate domain names for Amazon CloudFront distributions\. You can use this feature both for alternate domain names at the zone apex \(example\.com\) and alternate domain names for subdomains \(www\.example\.com\)\. For more information, see [Routing traffic to an Amazon CloudFront web distribution by using your domain name](routing-to-cloudfront-distribution.md)\.

**May 30, 2013**  
With this release, Route 53 adds support for evaluating the health of ELB load balancers and the associated Amazon EC2 instances\. For more information, see [Creating Amazon Route 53 health checks and configuring DNS failover](dns-failover.md)\.

**March 28, 2013**  
The documentation about health checks and failover was rewritten to enhance usability\. For more information, see [Creating Amazon Route 53 health checks and configuring DNS failover](dns-failover.md)\.

**February 11, 2013**  
With this release, Route 53 adds support for failover and health checks\. For more information, see [Creating Amazon Route 53 health checks and configuring DNS failover](dns-failover.md)\. 

## 2012 release<a name="doc-history-2012"></a>

**March 21, 2012**  
With this release, Route 53 lets you create latency records\. For more information, see [Latency\-based routing](routing-policy.md#routing-policy-latency)\.

## 2011 releases<a name="doc-history-2011"></a>

**December 21, 2011**  
With this release, the Route 53 console in the AWS Management Console lets you create an alias record by choosing an Elastic Load Balancer from a list instead of manually entering the hosted zone ID and the DNS name of the load balancer\. New functionality is documented in the *Amazon Route 53 Developer Guide*\.

**November 16, 2011**  
With this release, you can use the Route 53 console in the AWS Management Console to create and delete hosted zones, and to create, change, and delete records\. New functionality is documented throughout the *Amazon Route 53 Developer Guide*, as applicable\.

**October 18, 2011**  
The *Amazon Route 53 Getting Started Guide* was merged into the *Amazon Route 53 Developer Guide*, and the *Developer Guide* was reorganized to enhance usability\.

**May 24, 2011**  
This release of Amazon Route 53 introduces alias records, which allow you to create zone apex aliases; weighted records; a new API \(2011\-05\-05\); and a service\-level agreement\. In addition, after six months in beta, Route 53 is now generally available\. For more information, see the [Amazon Route 53 product page](https://aws.amazon.com/route53/) and [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md) in the *Amazon Route 53 Developer Guide*\.

## 2010 release<a name="doc-history-2010"></a>

**December 5, 2010**  
This is the first release of *Amazon Route 53 Developer Guide*\.