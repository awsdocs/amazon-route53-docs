# TTL \(time to live\)<a name="record-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you reduce the number of calls that DNS recursive resolvers must make to Route 53 to get the latest information in this record\. This has the effect of reducing latency and reducing your bill for Route 53 service\. 

However, if you specify a longer value for TTL, it takes longer for changes to the record \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods before they ask Route 53 for the latest information\. 

If you're associating this record with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\. 

## Learn more<a name="record-ttl-learn-more"></a>
+ [Working with Records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)