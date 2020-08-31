# Viewing DNS query metrics for a public hosted zone<a name="hosted-zone-public-viewing-query-metrics"></a>

You can view the total number of DNS queries that Route 53 is responding to for a specified public hosted zone or combination of public hosted zones\. The metrics appear in CloudWatch, which lets you view a graph, choose the time period that you want to view, and customize the metrics in a variety of other ways\. You can also create alarms and configure notifications, so that you're notified when the number of DNS queries in a specified time period go above or below a specified level\.

**Note**  
Route 53 automatically sends the number of DNS queries to CloudWatch for all public hosted zones, so you don't need to configure anything before you can view query metrics\. There's no charge for DNS query metrics\.

**Which DNS queries are counted?**  
Metrics include only the queries that DNS resolvers forward to Route 53\. If a DNS resolver has already cached the response to a query \(such as the IP address for a load balancer for example\.com\), the resolver will continue to return the cached response without forwarding the query to Route 53 until the TTL for the corresponding record expires\.  
Depending on how many DNS queries are submitted for a domain name \(example\.com\) or subdomain name \(www\.example\.com\), which resolvers your users are using, and the TTL for the record, DNS query metrics might contain information about only one query out of every several thousand queries that are submitted to DNS resolvers\. For more information about how DNS works, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\. 

**When do query metrics for a hosted zone start to appear in CloudWatch?**  
After you create a hosted zone, there's a delay of up to several hours before the hosted zone can appear in CloudWatch\. In addition, you must submit a DNS query for a record in the hosted zone so there's data to display\. 

**Metrics are available only in US East \(N\. Virginia\)**  
To get metrics on the console, you must choose US East \(N\. Virginia\) for the Region\. To get metrics using the AWS CLI, you must either leave the AWS Region unspecified, or specify `us-east-1` as the Region\. Route 53 metrics aren't available if you choose any other Region\.

**CloudWatch metric and dimension for DNS queries**  
For information about the CloudWatch metric and dimension for DNS queries, see [Monitoring hosted zones using Amazon CloudWatch](monitoring-hosted-zones-with-cloudwatch.md)\. For information about CloudWatch metrics, see [Using Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) in the *Amazon CloudWatch User Guide*\.

**Getting more detailed data about DNS queries**  
To get more detailed information about each DNS query that Route 53 responds to, including the following values, you can configure query logging:  
+ Domain or subdomain that was requested
+ Date and time of the request
+ DNS record type \(such as A or AAAA\)
+ Route 53 edge location that responded to the DNS query
+ DNS response code, such as `NoError` or `ServFail`
For more information, see [Public DNS query logging](query-logs.md)\.

**How to get DNS query metrics**  
Shortly after you create a hosted zone, Amazon Route 53 starts to send metrics and dimensions once a minute to CloudWatch\. You can use the following procedures to view the metrics on the CloudWatch console or view them by using the AWS Command Line Interface \(AWS CLI\)\.

**Topics**
+ [Viewing DNS query metrics for a public hosted zone in the CloudWatch console](#hosted-zone-public-viewing-query-metrics-console)
+ [Getting DNS query metrics using the AWS CLI](#hosted-zone-public-viewing-query-metrics-cli)

## Viewing DNS query metrics for a public hosted zone in the CloudWatch console<a name="hosted-zone-public-viewing-query-metrics-console"></a>

To view DNS query metrics for public hosted zones in the CloudWatch console, perform the following procedure\.<a name="hosted-zone-public-viewing-query-metrics-console-procedure"></a>

**To view DNS query metrics for a public hosted zone on the CloudWatch console**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Metrics**\.

1. On the AWS Region list in the upper right corner of the console, choose **US East \(N\. Virginia\)**\. Route 53 metrics aren't available if you choose any other AWS Region\.

1. On the **All metrics** tab, choose **Route 53**\.

1. Choose **Hosted Zone Metrics**\.

1. Select the check box for one or more hosted zones that have the metric name **DNSQueries**\.

1. On the **Graphed metrics** tab, change the applicable values to view the metrics in the format that you want\.

   For **Statistic**, choose **Sum** or **SampleCount**; these statistics both display the same value\.

## Getting DNS query metrics using the AWS CLI<a name="hosted-zone-public-viewing-query-metrics-cli"></a>

To get DNS query metrics using the AWS CLI, you use the [get\-metric\-data](https://docs.aws.amazon.com/cli/latest/reference/cloudwatch/get-metric-data.html) command\. Note the following:
+ You specify most values for the command in a separate JSON file\. For more information, see [get\-metric\-data](https://docs.aws.amazon.com/cli/latest/reference/cloudwatch/get-metric-data.html)\.
+ The command returns one value for each interval that you specify for `Period` in the JSON file\. `Period` is in seconds, so if you specify a five\-minute time period and specify `60` for `Period`, you get five values\. If you specify a five\-minute time period and specify `300` for `Period`, you get one value\. 
+ In the JSON file, you can specify any value for `Id`\.
+ Either leave the AWS Region unspecified, or specify `us-east-1` as the Region\. Route 53 metrics aren't available if you choose any other Region\. For more information, see [Configuring the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) in the *AWS Command Line Interface User Guide*\.

Here's the AWS CLI command that you use to get DNS query metrics for the five\-minute time period between 4:01 and 4:07 on May 1, 2019\. The `metric-data-queries` parameter references the sample JSON file that follows the command\.

```
aws cloudwatch get-metric-data --metric-data-queries file://./metric.json --start-time 2019-05-01T04:01:00Z --end-time 2019-05-01T04:07:00Z
```

Here's the sample JSON file:

```
[
    {
        "Id": "my_dns_queries_id",
        "MetricStat": {
            "Metric": {
                "Namespace": "AWS/Route53",
                "MetricName": "DNSQueries",
                "Dimensions": [
                    {
                        "Name": "HostedZoneId",
                        "Value": "Z1D633PJN98FT9"
                    }
                ]
            },
            "Period": 60,
            "Stat": "Sum"
        },
        "ReturnData": true
    }
]
```

Here's the output from this command\. Note the following:
+ The start time and end time in the command cover a seven\-minute time period, `2019-05-01T04:01:00Z` to `2019-05-01T04:07:00Z`\.
+ There are only six return values\. There's no value for `2019-05-01T04:05:00Z` because there were no DNS queries during that minute\.
+ The value of `Period` specified in the JSON file is `60` \(seconds\), so the values are reported in one\-minute intervals\.

```
{
    "MetricDataResults": [
        {
            "Id": "my_dns_queries_id",
            "StatusCode": "Complete",
            "Label": "DNSQueries",
            "Values": [
                101.0,
                115.0,
                103.0,
                127.0,
                111.0,
                120.0
            ],
            "Timestamps": [
                "2019-05-01T04:07:00Z",
                "2019-05-01T04:06:00Z",
                "2019-05-01T04:04:00Z",
                "2019-05-01T04:03:00Z",
                "2019-05-01T04:02:00Z",
                "2019-05-01T04:01:00Z"
            ]
        }
    ]
}
```