# How Health Checks Work in Simple Amazon Route 53 Configurations<a name="dns-failover-simple-configs"></a>

When you have two or more resources that perform the same function, such as two or more web servers for example\.com, you can use health checks to route traffic only to the healthy resources\. To use health checks in this simple configuration, you create a health check and a record for each resource, and you associate one health check with each record\. The health check regularly evaluates the status of the resource to see whether it's healthy\.

When Amazon Route 53 receives a DNS query for example\.com, it chooses one of the records and checks the status of the health check\. If the health check says the resource is healthy, Route 53 uses that record to route traffic to the corresponding resource\. If the health check says the resource is unhealthy, Route 53 chooses a different record and repeats the process\. 

Here's an overview of how you configure Route 53 to check the health of your resources in this simple configuration and how Route 53 responds to queries based on the health of your resources:

1. You identify the resources whose health you want Route 53 to monitor\. For example, you might want to monitor all of the HTTP servers that respond to requests for example\.com\.

1. You create health checks for your resources\. A health check tells Route 53 how to send requests to the endpoint whose health you want to check: which protocol to use \(HTTP, HTTPS, or TCP\), which IP address and port to use, and, for HTTP/HTTPS health checks, a domain name and path\. 

   A common configuration is to create one health check for each resource and to use the same IP address for the health check endpoint as for the resource\. If the IP address for your HTTP server is 192\.0\.2\.117, you create a health check for which the IP address is 192\.0\.2\.117\.
**Note**  
Route 53 cannot check the health of endpoints for which the IP address is in local, private, nonroutable, or multicast ranges\. For more information about IP addresses for which you cannot create health checks, see [RFC 5735, Special Use IPv4 Addresses](http://tools.ietf.org/html/rfc5735) and [RFC 6598, IANA\-Reserved IPv4 Prefix for Shared Address Space](http://tools.ietf.org/html/rfc6598)\.

   For more information about creating health checks by using the Route 53 console, see [Creating, Updating, and Deleting Health Checks](health-checks-creating-deleting.md)\. For information about creating health checks by using the Route 53 API, see [CreateHealthCheck](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html) in the *Amazon Route 53 API Reference*\.

1. You might need to configure router and firewall rules so that Route 53 can send regular requests to the endpoints that you specified in your health checks\. For more information, see [Configuring Router and Firewall Rules for Amazon Route 53 Health Checks](dns-failover-router-firewall-rules.md)\.

1. You create a group of records for your resources, for example, a group of weighted records that all have a type of A\. You associate the health checks that you created in step 2 with the corresponding records\. When you're finished, your configuration looks similar to the following diagram:  
![\[Three weighted records and corresponding health checks.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-weighted.png)

   For more information about creating records by using the Route 53 console, see [Creating Records by Using the Amazon Route 53 Console](resource-record-sets-creating.md)\. For information about creating records by using the Route 53 API, see [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

1. Route 53 periodically sends a request to each endpoint that you specified when you created your health checks; it doesn't perform the health check when it receives a DNS query\. Based on the responses, Route 53 decides whether the endpoints are healthy and uses that information to determine how to respond to queries\. For more information, see [How Amazon Route 53 Determines Whether an Endpoint Is Healthy](dns-failover-determining-health-of-endpoints.md)\.
**Important**  
Route 53 doesn't check the health of the resource specified in the record, such as the IP address specified in an A record for example\.com\. When you associate a health check with a record, Route 53 begins to check the health of the endpoint that you specified in the health check\.

1. Here's what happens when Route 53 receives a query for example\.com:

   1. Route 53 chooses a record based on the routing policy\. In this case, it chooses a record based on weight\.

   1. It determines the current health of the selected record by checking the status of the health check for that record\.

   1. If the selected record is unhealthy, it repeats the process of choosing a record based on the routing policy\. This time, the unhealthy record isn't considered\. 

   1. It responds to the query with the selected healthy record\. 

The following example shows a group of weighted records in which the third record is unhealthy\. Initially, Route 53 selects a record based on the weights of all three records\. If it happens to select the unhealthy record the first time, Route 53 selects another record, but this time it omits the weight of the third record from the calculation:

+ When Route 53 initially selects from among all three records, it responds to requests using the first record about 20% of the time, 10/\(10 \+ 20 \+ 20\)\. 

+ When Route 53 determines that the third record is unhealthy, it responds to requests using the first record about 33% of the time, 10/\(10 \+ 20\)\.

![\[Three weighted records and corresponding health checks.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-weighted-failed-hc.png)

If you omit a health check from one or more records in a group of records, Route 53 treats those records as healthy\. Route 53 has no basis for determining the health of the corresponding resource and might choose a record for which the resource is unhealthy\.

![\[Three weighted records, only two of which have health checks.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-weighted-missing-health-check.png)