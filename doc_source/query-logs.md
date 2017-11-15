# Logging DNS Queries<a name="query-logs"></a>

You can configure Amazon Route 53 to log information about the queries that Amazon Route 53 receives, such as the following:

+ The domain or subdomain that was requested

+ The date and time of the request

+ The DNS record type \(such as A or AAAA\)

+ The Amazon Route 53 edge location that responded to the DNS query

+ The DNS response code, such as `NoError` or `ServFail`

When you configure query logging, Amazon Route 53 starts to send logs to CloudWatch Logs\. You use CloudWatch Logs tools to access the query logs\.

Query logs contain only the queries that DNS resolvers forward to Amazon Route 53\. If a DNS resolver has already cached the response to a query \(such as the IP address for a load balancer for example\.com\), the resolver will continue to return the cached response without forwarding the query to Amazon Route 53 until the TTL for the corresponding record expires\. 

Depending on how many DNS queries are submitted for a domain name \(example\.com\) or subdomain name \(www\.example\.com\), which resolvers your users are using, and the TTL for the record, query logs might contain information about only one query out of every several thousand queries that are submitted to DNS resolvers\. For more information about how DNS works, see [How Internet Traffic Is Routed to Your Website or Web Application](welcome-dns-service.md)\.


+ [Configuring Logging for DNS Queries](#query-logs-configuring)
+ [Using Amazon CloudWatch to Access DNS Query Logs](#query-logs-viewing)
+ [Changing the Retention Period for Logs and Exporting Logs to Amazon S3](#query-logs-changing-retention-period)
+ [Stopping Query Logging](#query-logs-deleting-configuration)
+ [Format of DNS Query Logs](#query-logs-format)

## Configuring Logging for DNS Queries<a name="query-logs-configuring"></a>

To start logging DNS queries for a specified hosted zone, you perform the following tasks in the Amazon Route 53 console:

+ Choose the CloudWatch Logs log group that you want Amazon Route 53 to publish logs to, or create a new log group\.
**Note**  
The log group must be in the US East \(N\. Virginia\) Region\.

+ Choose to use existing CloudWatch Logs resource policies or create a new one\. Amazon Route 53 needs permission to publish logs to a log group, and resource policies grant the required permissions\.

+ Create a query logging configuration\.

**Note**  
If users are submitting DNS queries for your domain, you should start to see queries in the logs within a few minutes after you create the query logging configuration\. 

**To configure logging for DNS queries**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. Choose the radio button \(not the name\) for the hosted zone that you want to configure logging for\.

1. In the **Hosted zone details** pane, choose **Configure query logging**\.

1. Choose whether you want Amazon Route 53 to publish logs to an existing CloudWatch Logs log group or to a new log group\.

1. Either type a name for the new log group or choose an existing log group from the list\.
**Important**  
If you want to configure logging for multiple hosted zones, we recommend that you use a consistent prefix for every log group, for example:   
`/aws/route53/`*hosted\-zone\-name*  
On the next page of the wizard, you'll choose a CloudWatch Logs resource policy, which grants permission to Amazon Route 53 to publish logs to the log group\. For each resource policy, you must specify the log groups that it applies to\. There's a limit \(currently 10\) on the number of resource policies that you can create for an AWS account\. If you use a consistent prefix for the names of your log groups, then you can use one resource policy for all of your Amazon Route 53 hosted zones\. For example, if your log group names all begin with `/aws/route53/`, you can create a resource policy that applies to `/aws/route53/*`\. Then you can use the resource policy for the log groups for all of your hosted zones\. 

1. Choose **Next**\.

1. Choose whether to use existing CloudWatch Logs resource policies or create a new one\.
**Note**  
Amazon Route 53 can use the permissions in any existing resource policy\. When you choose to use existing resource policies, you don't need to choose a specific resource policy\.

1. If you chose to use existing resource policies, perform the following steps\. If you chose to create a new resource policy, skip to step 10\.

   1. Choose **Test** to determine whether any of your existing resource policies grant the permissions that Amazon Route 53 needs to publish logs to the log group that you chose or created on the previous page\.

   1. If the test fails, do one of the following:

      + Choose the option to create a new resource policy, and skip to step 10\.

      + Choose **Edit** for one of the existing resource policies, and change the value of **Log groups that the resource policy applies to**\. Specify either the name of a log group \(such as **/aws/route53/example\.com**\) or a value that includes the current log group \(such as **/aws/route53/\***\)\. You can use the wildcard character \(`*`\) to replace 0 or more characters in the name of the log group\.

        To view the settings for a resource policy, choose the arrow on the left side of the resource policy name\.

   1. Continue to edit **Log groups that the resource policy applies to** and retest until the test passes\. 

   1. Skip to step 11\.

1. If you chose to create a resource policy, perform the following steps:

   1. For **Resource policy name**, type a name for the resource policy\.

   1. For **Log groups that the resource policy applies to**, type a value that includes the log group that you chose or created on the previous page\. The name of that log group is at the top of the current page\.

      You can include the wildcard character \(`*`\) to replace 0 or more characters in the name of the log group, for example, `/aws/route53/*`\.

   1. Choose **Create policy and test permissions** to determine whether the new resource policy or any of your existing resource policies grant the permissions that Amazon Route 53 needs to publish logs to the log group that you chose or created on the previous page\.

   1. If the test fails, choose **Edit** for one of the existing resource policies, and change the value of **Log groups that the resource policy applies to**\. Specify either the name of a log group \(such as **/aws/route53/example\.com**\) or a value that includes the current log group \(such as **/aws/route53/\***\)\. You can use the wildcard character \(`*`\) to replace 0 or more characters in the name of the log group\.

      To view the settings for a resource policy, choose the arrow on the left side of the resource policy name\.

   1. Continue to edit **Log groups that the resource policy applies to** and retest until the test passes\. 

   1. Continue with step 11\.

1. Choose **Create query logging config**\.

## Using Amazon CloudWatch to Access DNS Query Logs<a name="query-logs-viewing"></a>

Amazon Route 53 sends query logs directly to CloudWatch Logs; the logs are never accessible through Amazon Route 53\. Instead, you use CloudWatch Logs to view logs in near real\-time, search and filter data, and export logs to Amazon S3\. 

Amazon Route 53 creates one CloudWatch Logs log stream for each Amazon Route 53 edge location that responds to DNS queries for the specified hosted zone and sends query logs to the applicable log stream\. The format for the name of each log stream is *hosted\-zone\-id*/*edge\-location\-ID*, for example, `Z1D633PJN98FT9/DFW3`\.

Each edge location is identified by a three\-letter code and an arbitrarily assigned number, for example, DFW3\. The three\-letter code typically corresponds with the International Air Transport Association airport code for an airport near the edge location\. \(These abbreviations might change in the future\.\) For a list of edge locations, see "The Amazon Route 53 Global Network" on the [Amazon Route 53 Product Details](https://aws.amazon.com/route53/details/) page\. 

For more information, see the applicable documentation:

+ [Amazon CloudWatch Logs User Guide](http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/)

+ [Amazon CloudWatch Logs API Reference](http://docs.aws.amazon.com/AmazonCloudWatchLogs/latest/APIReference/)

+ [CloudWatch Logs section of the AWS Command Line Interface Reference](http://docs.aws.amazon.com/cli/latest/reference/logs/index.html)

+ [Format of DNS Query Logs](#query-logs-format)

## Changing the Retention Period for Logs and Exporting Logs to Amazon S3<a name="query-logs-changing-retention-period"></a>

By default, CloudWatch Logs stores query logs indefinitely\. You can optionally specify a retention period so that CloudWatch Logs deletes logs that are older than the retention period\. For more information, see [Change Log Data Retention in CloudWatch Logs](http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SettingLogRetention.html) in the *Amazon CloudWatch User Guide*\.

If you want to retain log data but you don't need CloudWatch Logs tools to view and analyze the data, you can export logs to Amazon S3, which can reduce your storage costs\. For more information, see [Exporting Log Data to Amazon S3](http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/S3Export.html)\.

For information about pricing, see the applicable pricing page:

+ "Amazon CloudWatch Logs" on the [CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing) page

+ [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing)

**Note**  
When you configure Amazon Route 53 to log DNS queries, you don't incur any Amazon Route 53 charges\.

## Stopping Query Logging<a name="query-logs-deleting-configuration"></a>

If you want Amazon Route 53 to stop sending query logs to CloudWatch Logs, perform the following procedure to delete the query logging configuration\. 

**To delete a query logging configuration**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. Choose the radio button \(not the name\) for the hosted zone that you want to delete the query logging configuration for\.

1. In the **Hosted zone details** pane, under **Query logging**, choose **Delete**\.

1. Choose **Delete** to confirm\.

## Format of DNS Query Logs<a name="query-logs-format"></a>

Each log file contains one log entry for each DNS query that Amazon Route 53 received from DNS resolvers in the corresponding edge location\. Each log entry includes the following values:

**Log format version**  
The version number of this query log\. If we add fields to the log or change the format of existing fields, we'll increment this value\.

**Query timestamp**  
The date and time that Amazon Route 53 responded to the request, in ISO 8601 format and Coordinated Universal Time \(UTC\), for example, `2017-03-16T19:20:25.177Z`\.   
For information about ISO 8601 format, see the Wikipedia article [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)\. For information about UTC, see the Wikipedia article [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)\.

**Hosted zone ID**  
The ID of the hosted zone that is associated with all the DNS queries in this log\.

**Query name**  
The domain or subdomain that was specified in the request\.

**Query type**  
Either the DNS record type that was specified in the request, or `ANY`\. For information about the types that Amazon Route 53 supports, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

**Response code**  
The DNS response code that Amazon Route 53 returned in response to the DNS query\. 

**Layer 4 protocol**  
The protocol that was used to submit the query, either `TCP` or `UDP`\.

**Amazon Route 53 edge location**  
The Amazon Route 53 edge location that responded to the query\. Each edge location is identified by a three\-letter code and an arbitrary number, for example, DFW3\. The three\-letter code typically corresponds with the International Air Transport Association airport code for an airport near the edge location\. \(These abbreviations might change in the future\.\)  
For a list of edge locations, see "The Amazon Route 53 Global Network" on the [Amazon Route 53 Product Detail](https://aws.amazon.com/route53/details/) page\.

**Resolver IP address**  
The IP address of the DNS resolver that submitted the request to Amazon Route 53\.

**EDNS client subnet**  
A partial IP address for the client that the request originated from, if available from the DNS resolver\.  
For more information, see the IETF draft [Client Subnet in DNS Requests](http://tools.ietf.org/html/draft-vandergaast-edns-client-subnet-02)\.