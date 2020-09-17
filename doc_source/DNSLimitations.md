# Quotas<a name="DNSLimitations"></a>

Amazon Route 53 API requests and entities are subject to the following quotas \(formerly referred to as "limits"\)\.

**Topics**
+ [Using Service Quotas to view and manage quotas](#limits-service-quotas)
+ [Quotas on entities](#limits-api-entities)
+ [Maximums on API requests](#limits-api-requests)

## Using Service Quotas to view and manage quotas<a name="limits-service-quotas"></a>

You can use the Service Quotas service to view quotas and to request quota increases for many AWS services\. For more information, see the [Service Quotas User Guide](https://docs.aws.amazon.com/servicequotas/latest/userguide/)\. \(You can currently use Service Quotas to view and manage only Route 53 and Route 53 Resolver quotas\. Domain registration quotas aren't available\.\) 

**Note**  
To view quotas and request higher quotas for Route 53, you must change the Region to US East \(N\. Virginia\)\. To view quotas and request higher quotas for Resolver, change to the applicable Region\.

## Quotas on entities<a name="limits-api-entities"></a>

Amazon Route 53 entities are subject to the following quotas\.

For information on getting current quotas \(formerly referred to as "limits"\), see the following Route 53 actions:
+ [GetAccountLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetAccountLimit.html) – Gets quotas on health checks, hosted zones, reusable delegation sets, traffic flow policies, and traffic flow policy records
+ [GetHostedZoneLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneLimit.html) – Gets quotas on records in a hosted zone and on Amazon VPCs that you can associate with a private hosted zone
+ [GetReusableDelegationSetLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetReusableDelegationSetLimit.html) – Gets the quota on the number of hosted zones that you can associate with a reusable delegation set

**Topics**
+ [Quotas on domains](#limits-api-entities-domains)
+ [Quotas on hosted zones](#limits-api-entities-hosted-zones)
+ [Quotas on records](#limits-api-entities-records)
+ [Quotas on Route 53 Resolver](#limits-api-entities-resolver)
+ [Quotas on health checks](#limits-api-entities-health-checks)
+ [Quotas on query log configurations](#limits-api-entities-query-log-configs)
+ [Quotas on traffic flow policies and policy records](#limits-api-entities-traffic-flow)
+ [Quotas on reusable delegation sets](#limits-api-entities-reusable-delegation-sets)

### Quotas on domains<a name="limits-api-entities-domains"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Domains | 50 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 

### Quotas on hosted zones<a name="limits-api-entities-hosted-zones"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Hosted zones | 500 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| Hosted zones that can use the same reusable delegation set  | 100 [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| Amazon VPCs that you can associate with a private hosted zone | 100 [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| Private hosted zones that you can associate a VPC with | No quota **\*** | 
| Authorizations that you can create so you can associate VPCs that were created by one account with a hosted zone that was created by another account | 100 | 

**\*** You can associate a VPC with any or all of the private hosted zones that you control through your AWS accounts\. For example, suppose you have three AWS accounts and all three have the default quota of 500 hosted zones\. If you create 500 private hosted zones for all three accounts, you can associate a VPC with all 1,500 private hosted zones\.

### Quotas on records<a name="limits-api-entities-records"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Records | 10,000 per hosted zone [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\. For a quota greater than 10,000 records in a hosted zone, an additional charge applies\.  | 
| Values in a record | 400 per record | 
| Geolocation, latency, multivalue answer, and weighted records | 100 records that have the same name and type | 
| Geoproximity records | 30 records that have the same name and type | 

### Quotas on Route 53 Resolver<a name="limits-api-entities-resolver"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Endpoints per AWS Region | 4 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| IP addresses per endpoint | 6 | 
| IP addresses per rule | 6 | 
| Rules per AWS Region | 1000 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| Associations between rules and VPCs per AWS Region | 2000 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| Queries per second per IP address in an endpoint | 10,000\* | 
|  Query log configurations per AWS Region  |  20  | 
|  Query log configuration VPC associations per AWS Region  |  100  | 
|  Query log configuration VPC associations per AWS Region \(shared using RAM\)  |  100  | 

**\*** The number of DNS queries per second \(QPS\) varies by the type of query, the size of the response, and the protocol in use\. This limit is on a per elastic network interface \(ENI\) basis\. For example, with a limit of 10,000 QPS, 2 ENIs would allow 20,000 QPS\. From there you can scale out by adding more ENIs\. For information about how to view Amazon CloudWatch metrics for IP addresses for inbound and outbound endpoints, see [Metrics for Resolver IP addresses](monitoring-resolver-with-cloudwatch.md#cloudwatch-metrics-resolver-ip-address)\.

### Quotas on health checks<a name="limits-api-entities-health-checks"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Health checks | 200 active health checks per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| Child health checks that a calculated health check can monitor | 255 | 
| Maximum total length of headers in the response to a health check request | 16,384 bytes \(16K\) | 

### Quotas on query log configurations<a name="limits-api-entities-query-log-configs"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Query log configurations | 1 per hosted zone | 

### Quotas on traffic flow policies and policy records<a name="limits-api-entities-traffic-flow"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Traffic policies For more information about Route 53 traffic flow, see [Using traffic flow to route DNS traffic](traffic-flow.md)\. | 50 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 
| Traffic policy versions | 1,000 per traffic policy | 
| Traffic policy records \(referred to as "policy instances" in the Route 53 API, AWS SDKs, AWS Command Line Interface, and AWS Tools for Windows PowerShell\) | 5 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 

### Quotas on reusable delegation sets<a name="limits-api-entities-reusable-delegation-sets"></a>


****  

| Entity | Quota | 
| --- | --- | 
| Reusable delegation sets | 100 per AWS account [Request a higher quota](https://console.aws.amazon.com/servicequotas/home?region=us-east-1#!/services/route53/quotas)\.  | 

## Maximums on API requests<a name="limits-api-requests"></a>

Amazon Route 53 API requests are subject to the following maximums\.

**Topics**
+ [Number of elements and characters in `ChangeResourceRecordSets` requests](#limits-api-requests-changeresourcerecordsets)
+ [Frequency of Amazon Route 53 API requests](#limits-api-requests-route-53)
+ [Frequency of Route 53 Resolver API requests](#limits-api-requests-route-53-resolver)

### Number of elements and characters in `ChangeResourceRecordSets` requests<a name="limits-api-requests-changeresourcerecordsets"></a>

**`ResourceRecord` elements**  
A request cannot contain more than 1,000 `ResourceRecord` elements\. When the value of the `Action` element is `UPSERT`, each `ResourceRecord` element is counted twice\.

**Maximum number of characters**  
The sum of the number of characters \(including spaces\) in all `Value` elements in a request cannot exceed 32,000 characters\. When the value of the `Action` element is `UPSERT`, each character in a `Value` element is counted twice\.

### Frequency of Amazon Route 53 API requests<a name="limits-api-requests-route-53"></a>

**All requests**  
Five requests per second per AWS account\. If you submit more than five requests per second, Amazon Route 53 returns an HTTP 400 error \(`Bad request`\)\. The response header also includes a `Code` element with a value of `Throttling` and a `Message` element with a value of `Rate exceeded`\.  
If your application exceeds this limit, we recommend that you implement exponential backoff for retries\. For more information, see [Error Retries and Exponential Backoff in AWS](https://docs.aws.amazon.com/general/latest/gr/api-retries.html) in the *Amazon Web Services General Reference*\.

**`ChangeResourceRecordSets` requests**  
If Route 53 can't process a request before the next request arrives, it will reject subsequent requests for the same hosted zone and return an HTTP 400 error \(`Bad request`\)\. The response header also includes a `Code` element with a value of `PriorRequestNotComplete` and a `Message` element with a value of `The request was rejected because Route 53 was still processing a prior request.`

**`CreateHealthCheck` requests**  
You can submit a maximum of 1,000 `CreateHealthCheck` requests in a 24\-hour period\.

### Frequency of Route 53 Resolver API requests<a name="limits-api-requests-route-53-resolver"></a>

**All requests**  
Five requests per second per AWS account per Region\. If you submit more than five requests per second in a Region, Resolver returns an HTTP 400 error \(`Bad request`\)\. The response header also includes a `Code` element with a value of `Throttling` and a `Message` element with a value of `Rate exceeded`\.  
If your application exceeds this limit, we recommend that you implement exponential backoff for retries\. For more information, see [Error Retries and Exponential Backoff in AWS](https://docs.aws.amazon.com/general/latest/gr/api-retries.html) in the *Amazon Web Services General Reference*\.