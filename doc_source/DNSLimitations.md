# Limits<a name="DNSLimitations"></a>

Amazon Route 53 API requests and entities are subject to the following limits\.


+ [Limits on API Requests](#limits-api-requests)
+ [Limits on Entities](#limits-api-entities)

## Limits on API Requests<a name="limits-api-requests"></a>

Amazon Route 53 API requests are subject to the following limits\.

### Number of Elements and Characters in `ChangeResourceRecordSets` Requests<a name="limits-api-requests-changeresourcerecordsets"></a>

**`ResourceRecord` elements**  
A request cannot contain more than 1000 `ResourceRecord` elements\. When the value of the `Action` element is `UPSERT`, each `ResourceRecord` element is counted twice\.

**Maximum number of characters**  
The sum of the number of characters \(including spaces\) in all `Value` elements in a request cannot exceed 32,000 characters\. When the value of the `Action` element is `UPSERT`, each character in a `Value` element is counted twice\.

### Frequency of Amazon Route 53 API Requests<a name="limits-api-requests-route-53"></a>

**All requests**  
Five requests per second per AWS account\. If you submit more than five requests per second, Amazon Route 53 returns an HTTP 400 error \(`Bad request`\)\. The response header also includes a `Code` element with a value of `Throttling` and a `Message` element with a value of `Rate exceeded`\.

**`ChangeResourceRecordSets` requests**  
If Amazon Route 53 can't process a request before the next request arrives, it will reject subsequent requests for the same hosted zone and return an HTTP 400 error \(`Bad request`\)\. The response header also includes a `Code` element with a value of `PriorRequestNotComplete` and a `Message` element with a value of `The request was rejected because Route 53 was still processing a prior request.`

**`CreateHealthCheck` requests**  
You can submit a maximum of 1000 `CreateHealthCheck` requests in a 24\-hour period\.

## Limits on Entities<a name="limits-api-entities"></a>

Amazon Route 53 entities are subject to the following limits\.


****  

| Entity | Limit | 
| --- | --- | 
| Hosted zones | 500 per AWS account [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Domains | 50 per AWS account [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Reusable delegation sets | 100 per AWS account [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Hosted zones that can use the same reusable delegation set  | 100 [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Amazon VPCs that you can associate with a private hosted zone | 100 [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Authorizations that you can create so you can associate Amazon VPCs that were created by one account with a hosted zone that was created by another account | 100 | 
| Resource record sets | 10,000 per hosted zone [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. For a limit greater than 10,000 resource record sets in a hosted zone, an additional charge applies\.  | 
| Resource records \(values in a resource record set\) | 100 per resource record set | 
| Weighted and geolocation resource record sets | 100 resource record sets that have the same name and type | 
| Health checks | 200 active health checks per AWS account [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Traffic flow traffic policies \(For more information about Amazon Route 53 traffic flow, see [Using Traffic Flow to Route DNS Traffic](traffic-flow.md)\.\) | 50 per AWS account [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Traffic flow policy records \(referred to as "policy instances" in the Amazon Route 53 API, AWS SDKs, AWS Command Line Interface, and AWS Tools for Windows PowerShell\) | 5 per AWS account [Request a higher limit](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-route53)\. | 
| Query log configurations | 1 per hosted zone | 