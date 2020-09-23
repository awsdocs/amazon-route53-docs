# Configure query logging<a name="query-logs"></a>

You can configure Route 53 to log information about the queries that it receives, such as the following:
+ Domain or subdomain that was requested
+ Date and time of the request
+ DNS record type \(such as A or AAAA\)
+ Route 53 edge location that responded to the DNS query
+ DNS response code, such as `NoError` or `ServFail`

When you configure query logging, Route 53 starts to send logs to CloudWatch Logs\. You use CloudWatch Logs tools to access the query logs\.

**Note**  
Query logging is available only for public hosted zones\.

## Learn more<a name="query-logs-learn-more"></a>
+ [Logging DNS queries](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/query-logs.html)