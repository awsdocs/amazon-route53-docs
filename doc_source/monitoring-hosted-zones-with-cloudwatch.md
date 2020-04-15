# Monitoring hosted zones using Amazon CloudWatch<a name="monitoring-hosted-zones-with-cloudwatch"></a>

You can monitor your public hosted zones by using Amazon CloudWatch to collect and process raw data into readable, near real\-time metrics\. Metrics are available shortly after Route 53 receives the DNS queries that the metrics are based on\. CloudWatch metric data for Route 53 hosted zones has a granularity of one minute\.

For more information, see the following documentation
+ For an overview and information about how to view metrics in the Amazon CloudWatch console and how to retrieve metrics using the AWS Command Line Interface \(AWS CLI\), see [Viewing DNS query metrics for a public hosted zone](hosted-zone-public-viewing-query-metrics.md)
+ For information about the retention period for metrics, see [GetMetricStatistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_GetMetricStatistics.html) in the *Amazon CloudWatch API Reference*\.
+ For more information about CloudWatch, see [What is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.
+ For more information about CloudWatch metrics, see [Using Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) in the *Amazon CloudWatch User Guide*\.

**Topics**
+ [CloudWatch metric for Route 53 public hosted zones](#cloudwatch-metrics-route-53-hosted-zones)
+ [CloudWatch dimension for Route 53 public hosted zone metrics](#cloudwatch-dimensions-route-53-hosted-zones)

## CloudWatch metric for Route 53 public hosted zones<a name="cloudwatch-metrics-route-53-hosted-zones"></a>

The `AWS/Route53` namespace includes the following metric for Route 53 hosted zones:

**DNSQueries**  
For all the records in a hosted zone, the number of DNS queries that Route 53 responds to in a specified time period\.  
Valid statistics: Sum, SampleCount  
Units: Count  
Region: Route 53 is a global service\. To get hosted zone metrics, you must specify US East \(N\. Virginia\) for the Region\. 

## CloudWatch dimension for Route 53 public hosted zone metrics<a name="cloudwatch-dimensions-route-53-hosted-zones"></a>

Route 53 metrics for hosted zones use the `AWS/Route53` namespace and provide metrics for `HostedZoneId`\. To get the number of DNS queries, you must specify the ID of the hosted zone in the `HostedZoneId` dimension\.