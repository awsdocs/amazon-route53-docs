# Public DNS query logging<a name="query-logs"></a>

You can configure Amazon Route 53 to log information about the public DNS queries that Route 53 receives, such as the following:
+ Domain or subdomain that was requested
+ Date and time of the request
+ DNS record type \(such as A or AAAA\)
+ Route 53 edge location that responded to the DNS query
+ DNS response code, such as `NoError` or `ServFail`

Once you configure query logging, Route 53 will send logs to CloudWatch Logs\. You use CloudWatch Logs tools to access the query logs\.

**Note**  
Query logging is also available for private hosted zones\. For more information, see [Resolver query logging](resolver-query-logs.md)\.

Query logs contain only the queries that DNS resolvers forward to Route 53\. If a DNS resolver has already cached the response to a query \(such as the IP address for a load balancer for example\.com\), the resolver will continue to return the cached response without forwarding the query to Route 53 until the TTL for the corresponding record expires\. 

Depending on how many DNS queries are submitted for a domain name \(example\.com\) or subdomain name \(www\.example\.com\), which resolvers your users are using, and the TTL for the record, query logs might contain information about only one query out of every several thousand queries that are submitted to DNS resolvers\. For more information about how DNS works, see [How internet traffic is routed to your website or web application](welcome-dns-service.md)\.

If you don't need detailed logging information, you can use Amazon CloudWatch metrics to see the total number of DNS queries that Route 53 responds to for a hosted zone\. For more information, see [Viewing DNS query metrics for a public hosted zone](hosted-zone-public-viewing-query-metrics.md)\.

**Topics**
+ [Configuring logging for DNS queries](#query-logs-configuring)
+ [Using Amazon CloudWatch to access DNS query logs](#query-logs-viewing)
+ [Changing the retention period for logs and exporting logs to Amazon S3](#query-logs-changing-retention-period)
+ [Stopping query logging](#query-logs-deleting-configuration)
+ [Values that appear in DNS query logs](#query-logs-format)
+ [Query log example](#query-logs-example)

## Configuring logging for DNS queries<a name="query-logs-configuring"></a>

To start logging DNS queries for a specified hosted zone, you perform the following tasks in the Amazon Route 53 console:
+ Choose the CloudWatch Logs log group that you want Route 53 to publish logs to, or create a new log group\.
**Note**  
The log group must be in the US East \(N\. Virginia\) Region\.
+ Choose **Create** to finish\.

**Note**  
If users are submitting DNS queries for your domain, you should start to see queries in the logs within a few minutes after you create the query logging configuration\. <a name="query-logs-configuring-procedure"></a>

**To configure logging for DNS queries**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. Choose the hosted zone that you want to configure query logging for\.

1. In the **Hosted zone details** pane, choose **Configure query logging**\.

1. Choose an existing log group or create a new log group\.

1. If you receive an alert about permissions \(this happens if you haven't configured query logging with the new console before\), do one of the following:
   +  If you have 10 resource policies already, you can't create any more\. Select any of your resource policies, and select **Edit **\. Editing will give Route 53 permissions to write logs to your log groups\. Choose **Save**\. The alert goes away and you can continue to the next step\. 
   + If you have never configured query logging before \(or if you haven't created 10 resource policies already\), you need to grant permissions to Route 53 to write logs to your CloudWatch Logs groups\. Choose **Grant permissions**\. The alert goes away and you can continue to the next step\. 

1. Choose **Permissions \- optional** to see a table that shows whether the resource policy matches the CloudWatch log group, and whether the Route 53 has the permission to publish logs to CloudWatch\.

1. Choose **Create**\.

## Using Amazon CloudWatch to access DNS query logs<a name="query-logs-viewing"></a>

Amazon Route 53 sends query logs directly to CloudWatch Logs; the logs are never accessible through Route 53\. Instead, you use CloudWatch Logs to view logs in near real\-time, search and filter data, and export logs to Amazon S3\. 

Route 53 creates one CloudWatch Logs log stream for each Route 53 edge location that responds to DNS queries for the specified hosted zone and sends query logs to the applicable log stream\. The format for the name of each log stream is *hosted\-zone\-id*/*edge\-location\-ID*, for example, `Z1D633PJN98FT9/DFW3`\.

Each edge location is identified by a three\-letter code and an arbitrarily assigned number, for example, DFW3\. The three\-letter code typically corresponds with the International Air Transport Association airport code for an airport near the edge location\. \(These abbreviations might change in the future\.\) For a list of edge locations, see "The Route 53 Global Network" on the [Route 53 Product Details](https://aws.amazon.com/route53/details/) page\. 

For more information, see the applicable documentation:
+ [Amazon CloudWatch Logs User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/)
+ [Amazon CloudWatch Logs API Reference](https://docs.aws.amazon.com/AmazonCloudWatchLogs/latest/APIReference/)
+ [CloudWatch Logs section of the AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/reference/logs/index.html)
+ [Values that appear in DNS query logs](#query-logs-format)

## Changing the retention period for logs and exporting logs to Amazon S3<a name="query-logs-changing-retention-period"></a>

By default, CloudWatch Logs stores query logs indefinitely\. You can optionally specify a retention period so that CloudWatch Logs deletes logs that are older than the retention period\. For more information, see [Change log data retention in CloudWatch Logs](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SettingLogRetention.html) in the *Amazon CloudWatch User Guide*\.

If you want to retain log data but you don't need CloudWatch Logs tools to view and analyze the data, you can export logs to Amazon S3, which can reduce your storage costs\. For more information, see [Exporting log data to Amazon S3](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/S3Export.html)\.

For information about pricing, see the applicable pricing page:
+ "Amazon CloudWatch Logs" on the [CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing) page
+ [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing)

**Note**  
When you configure Route 53 to log DNS queries, you don't incur any Route 53 charges\.

## Stopping query logging<a name="query-logs-deleting-configuration"></a>

If you want Amazon Route 53 to stop sending query logs to CloudWatch Logs, perform the following procedure to delete the query logging configuration\. <a name="query-logs-deleting-configuration-procedure"></a>

**To delete a query logging configuration**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. Choose the name for the hosted zone that you want to delete the query logging configuration for\.

1. In the **Hosted zone details** pane, choose **Delete query logging configuration**\.

1. Choose **Delete** to confirm\.

## Values that appear in DNS query logs<a name="query-logs-format"></a>

Each log file contains one log entry for each DNS query that Amazon Route 53 received from DNS resolvers in the corresponding edge location\. Each log entry includes the following values:

**Log format version**  
The version number of this query log\. If we add fields to the log or change the format of existing fields, we'll increment this value\.

**Query timestamp**  
The date and time that Route 53 responded to the request, in ISO 8601 format and Coordinated Universal Time \(UTC\), for example, `2017-03-16T19:20:25.177Z`\.   
For information about ISO 8601 format, see the Wikipedia article [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)\. For information about UTC, see the Wikipedia article [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)\.

**Hosted zone ID**  
The ID of the hosted zone that is associated with all the DNS queries in this log\.

**Query name**  
The domain or subdomain that was specified in the request\.

**Query type**  
Either the DNS record type that was specified in the request, or `ANY`\. For information about the types that Route 53 supports, see [Supported DNS record types](ResourceRecordTypes.md)\.

**Response code**  
The DNS response code that Route 53 returned in response to the DNS query\. 

**Layer 4 protocol**  
The protocol that was used to submit the query, either `TCP` or `UDP`\.

**Route 53 edge location**  
The Route 53 edge location that responded to the query\. Each edge location is identified by a three\-letter code and an arbitrary number, for example, DFW3\. The three\-letter code typically corresponds with the International Air Transport Association airport code for an airport near the edge location\. \(These abbreviations might change in the future\.\)  
For a list of edge locations, see "The Route 53 Global Network" on the [Route 53 Product Detail](https://aws.amazon.com/route53/details/) page\.

**Resolver IP address**  
The IP address of the DNS resolver that submitted the request to Route 53\.

**EDNS client subnet**  
A partial IP address for the client that the request originated from, if available from the DNS resolver\.  
For more information, see the IETF draft [Client Subnet in DNS Requests](https://tools.ietf.org/html/draft-ietf-dnsop-edns-client-subnet-08)\.

## Query log example<a name="query-logs-example"></a>

Here's an example query log:

```
1.0 2017-12-13T08:16:02.130Z Z123412341234 example.com A NOERROR UDP FRA6 192.168.1.1 -
1.0 2017-12-13T08:15:50.235Z Z123412341234 example.com AAAA NOERROR TCP IAD12 192.168.3.1 192.168.222.0/24
1.0 2017-12-13T08:16:03.983Z Z123412341234 example.com ANY NOERROR UDP FRA6 2001:db8::1234 2001:db8:abcd::/48
1.0 2017-12-13T08:15:50.342Z Z123412341234 bad.example.com A NXDOMAIN UDP IAD12 192.168.3.1 192.168.111.0/24
1.0 2017-12-13T08:16:05.744Z Z123412341234 txt.example.com TXT NOERROR UDP JFK5 192.168.1.2 -
```