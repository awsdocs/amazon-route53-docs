# Resolver query logging<a name="resolver-query-logs"></a>

You can log the DNS queries that originate in Amazon Virtual Private Cloud VPCs that you specify, as well as the responses to those DNS queries\. Resolver query logs include values such as the following:
+ The AWS Region where the VPC was created
+ The ID of the VPC that the query originated from
+ The IP address of the instance that the query originated from
+ The instance ID of the resource that the query originated from
+ The date and time that the query was first made
+ The DNS name requested \(such as prod\.example\.com\)
+ The DNS record type \(such as A or AAAA\)
+ The DNS response code, such as `NoError` or `ServFail`
+ The DNS response data, such as the IP address that is returned in response to the DNS query

For a detailed list of all of the values logged and an example, see [Values that appear in Resolver query logs](resolver-query-logs-format.md)\.

**Note**  
As is standard for DNS resolvers, resolvers cache DNS queries for a length of time determined by the time\-to\-live \(TTL\) for the resolver\. The Route 53 Resolver caches queries that originate in your VPCs, and responds from the cache whenever possible to speed up responses\. Resolver query logging logs only unique queries, not queries that Resolver is able to respond to from the cache\.  
For example, suppose that an EC2 instance in one of the VPCs that a query logging configuration is logging queries for, submits a request for accounting\.example\.com\. Resolver caches the response to that query, and logs the query\. If the same instance’s ENI makes a query for accounting\.example\.com within the TTL of the Resolver’s cache, Resolver responds to the query from the cache\. The second query is not logged\.

You can send the logs to one of the following AWS resources: 
+ Amazon CloudWatch Logs \(CloudWatch Logs\) log group
+ Amazon S3 \(S3\) bucket
+ Kinesis Data Firehose delivery stream

For more information, see [AWS resources that you can send Resolver query logs to](resolver-query-logs-choosing-target-resource.md)\.

**Topics**
+ [AWS resources that you can send Resolver query logs to](resolver-query-logs-choosing-target-resource.md)
+ [Managing Resolver query logging configurations](resolver-query-logging-configurations-managing.md)