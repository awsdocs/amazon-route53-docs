# Simple routing records to add to *domain\-name*<a name="routing-simple"></a>

The list of simple routing records that you have defined but not yet created in the hosted zone includes the following values:
+ **Record name**: Route 53 responds to DNS queries for this name\.
+ **Type**: The DNS record type determines the format of the value in the record\. For example, if the type is **A**, the value in the record is an IP address in IPv4 format, such as 192\.0\.2\.44\. See [Supported DNS record types](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/ResourceRecordTypes.html)\.
+ **Value/route traffic to**: For Route 53 alias records, this is the DNS name of the AWS resource that you're routing traffic to, such as a CloudFront distribution\. For other records, the value depends on the record type\. For example, for an A record, this is an IP address in IPv4 format, such as 192\.0\.2\.44\.
+ **TTL \(seconds\)**: The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you reduce the number of calls that DNS recursive resolvers must make to Route 53 to get the latest information in this record\. This has the effect of reducing latency and reducing your bill for Route 53 service\. 

  However, if you specify a longer value for TTL, it takes longer for changes to the record \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods before they ask Route 53 for the latest information\. 

  If you're associating this record with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\. 

## Learn more<a name="routing-simple-learn-more"></a>
+ [Working with Records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)