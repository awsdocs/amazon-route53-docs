# How health checks work in simple Amazon Route 53 configurations<a name="dns-failover-simple-configs"></a>

When you have two or more resources that perform the same function, such as two or more web servers for example\.com, you can use the following health\-checking features to route traffic only to the healthy resources:

**Check the health of EC2 instances and other resources \(non\-alias records\)**  
If you're routing traffic to resources that you can't create alias records for, such as EC2 instances, you create a record and a health check for each resource\. Then you associate each health check with the applicable record\. Health checks regularly check the health of the corresponding resources, and Route 53 routes traffic only to the resources that health checks report as healthy\.

**Evaluate the health of an AWS resource \(alias records\)**  
If you're using [alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) to route traffic to selected AWS resources, such as ELB load balancers, you can configure Route 53 to evaluate the health of the resource and to route traffic only to resources that are healthy\. When you configure an alias record to evaluate the health of a resource, you don't need to create a health check for the resource\.

Here's an overview of how you configure Route 53 to check the health of your resources in simple configurations:

1. You identify the resources that you want Route 53 to monitor\. For example, you might want to monitor all the HTTP servers that respond to requests for example\.com\.

1. You create health checks for the resources that you can't create alias records for, such as EC2 instances or servers in your own data center\. You specify how to send health\-checking requests to the resource: which protocol to use \(HTTP, HTTPS, or TCP\), which IP address and port to use, and, for HTTP/HTTPS health checks, a domain name and path\. 
**Note**  
If you're using any resources that you can create alias records for, such as ELB load balancers, don't create health checks for those resources\. 

   A common configuration is to create one health check for each resource and to use the same IP address for the health check endpoint as for the resource\. The health check sends requests to the specified IP address\.
**Note**  
Route 53 can't check the health of resources that have an IP address in local, private, nonroutable, or multicast ranges\. For more information about IP addresses that you can't create health checks for, see [RFC 5735, Special Use IPv4 Addresses](http://tools.ietf.org/html/rfc5735) and [RFC 6598, IANA\-Reserved IPv4 Prefix for Shared Address Space](http://tools.ietf.org/html/rfc6598)\.

   For more information about creating health checks, see [Creating, updating, and deleting health checks](health-checks-creating-deleting.md)\.

1. You might need to configure router and firewall rules so that Route 53 can send regular requests to the endpoints that you specified in your health checks\. For more information, see [Configuring router and firewall rules for Amazon Route 53 health checksConfiguring router and firewall rules for health checks](dns-failover-router-firewall-rules.md)\.

1. You create a group of records for your resources, for example, a group of weighted records\. You can mix alias and non\-alias records, but they all must have the same value for **Name**, **Type**, and **Routing Policy**\.

   How you configure Route 53 to check the health of your resources depends on whether you're creating alias records or non\-alias records:
   + **Alias records** – Specify **Yes** for **Evaluate Target Health**\.
   + **Non\-alias records** – Associate the health checks that you created in step 2 with the corresponding records\. 

   When you're finished, your configuration looks similar to the following diagram, which includes only non\-alias records\.  
![\[Three weighted records and corresponding health checks.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-weighted.png)

   For more information about creating records by using the Route 53 console, see [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)\. 

1. If you created health checks, Route 53 periodically sends requests to the endpoint for each health check; it doesn't perform the health check when it receives a DNS query\. Based on the responses, Route 53 decides whether the endpoints are healthy and uses that information to determine how to respond to queries\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

   Route 53 doesn't check the health of the resource specified in the record, such as the IP address that is specified in an A record for example\.com\. When you associate a health check with a record, Route 53 begins to check the health of the endpoint that you specified in the health check\. You can also configure Route 53 to monitor the health of other health checks or monitor the data streams for CloudWatch alarms\. For more information, see [Types of Amazon Route 53 health checksTypes of health checks](health-checks-types.md)\.

Here's what happens when Route 53 receives a query for example\.com:

1. Route 53 chooses a record based on the routing policy\. In this case, it chooses a record based on weight\.

1. It determines the current health of the selected record by checking the status of the health check for that record\.

1. If the selected record is unhealthy, Route 53 chooses a different record\. This time, the unhealthy record isn't considered\. 

   For more information, see [How Amazon Route 53 chooses records when health checking is configuredHow Route 53 chooses records when health checking is configured](health-checks-how-route-53-chooses-records.md)\.

1. When Route 53 finds a healthy record, it responds to the query with the applicable value, such as the IP address in an A record\. 

The following example shows a group of weighted records in which the third record is unhealthy\. Initially, Route 53 selects a record based on the weights of all three records\. If it happens to select the unhealthy record the first time, Route 53 selects another record, but this time it omits the weight of the third record from the calculation:
+ When Route 53 initially selects from among all three records, it responds to requests using the first record about 20% of the time, 10/\(10 \+ 20 \+ 20\)\. 
+ When Route 53 determines that the third record is unhealthy, it responds to requests using the first record about 33% of the time, 10/\(10 \+ 20\)\.

![\[Three weighted records and the corresponding health checks. The third health check is unhealthy, so Route 53 considers the associated record to be unhealthy.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-weighted-failed-hc.png)

If you omit a health check from one or more records in a group of records, Route 53 has no way to determine the health of the corresponding resource\. Route 53 treats those records as healthy\.

![\[Three weighted records, only two of which have health checks. Route 53 always considers the third record to be healthy.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-weighted-missing-health-check.png)