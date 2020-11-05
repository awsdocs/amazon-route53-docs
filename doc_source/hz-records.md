# Records<a name="hz-records"></a>

The list of records for a hosted zone includes the following information:
+ **Record name**: Route 53 responds to DNS queries for this name\.
+ **Type**: The DNS record type determines the format of the value in the record\. For example, if the type is **A**, the value in the record is an IP address in IPv4 format, such as 192\.0\.2\.44\. See [Supported DNS record types](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html)\.
+ **Routing policy**: A record with a routing policy of **Simple** is a standard DNS record\. All other routing policies route traffic using Route 53–specific features\. See [Choosing a routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)\.
+ **Differentiator**: For routing policies other than Simple, this value depends on the routing policy\. For example, for weighted records, Differentiator is the weight\. For latency records, it's an AWS Region that you have a resource in, such as an EC2 instance\. 
+ **Value/route traffic to**: For Route 53 alias records, this is the DNS name of the AWS resource that you're routing traffic to, such as a CloudFront distribution\. For other records, the value depends on the record type\. For example, for an A record, this is an IP address in IPv4 format, such as 192\.0\.2\.44\.

## Learn more<a name="hz-records-learn-more"></a>
+ [Supported DNS record types](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html)
+ [Choosing a routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)
+ [Values that you specify when you create or edit Amazon Route 53 records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-values.html)