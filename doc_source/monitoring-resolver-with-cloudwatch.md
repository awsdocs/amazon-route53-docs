# Monitoring Route 53 Resolver endpoints with Amazon CloudWatch<a name="monitoring-resolver-with-cloudwatch"></a>

You can use Amazon CloudWatch to monitor the number of DNS queries that are forwarded by Route 53 Resolver endpoints\. Amazon CloudWatch collects and processes raw data into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your resources are performing\. By default, metric data for Resolver endpoints is automatically sent to CloudWatch at five\-minute intervals\.

For more information about Resolver, see [Resolving DNS queries between VPCs and your network](resolver.md)\. For more information about CloudWatch, see [What is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

## Metrics and dimensions for Route 53 Resolver<a name="metrics-dimensions-resolver"></a>

When you configure Resolver to forward DNS queries to your network or vice versa, Resolver starts to send [metrics](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/monitoring-resolver-with-cloudwatch.html#cloudwatch-metrics-resolver) and [dimensions](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/monitoring-resolver-with-cloudwatch.html#cloudwatch-dimensions-resolver) once every five minutes to CloudWatch about the number of queries that are forwarded\. You can use the following procedures to view the metrics in the CloudWatch console or view them by using the AWS Command Line Interface \(AWS CLI\)\.

**To view Resolver metrics using the CloudWatch console**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. On the navigation bar, choose the Region where you created the endpoint\.

1. In the navigation pane, choose **Metrics**\.

1. On the **All metrics** tab, choose **Route 53 Resolver**\.

1. Choose **By Endpoint** to view query counts for a specified endpoint\. Then choose the endpoints that you want to view the number of queries for\. 

   Choose **Across All Endpoints** to view query counts for all inbound endpoints or for all outbound endpoints that were created by the current AWS account\. Then choose **InboundQueryVolume** or **OutboundQueryVolume** to view the desired counts\.

**To view metrics using the AWS CLI**
+ At a command prompt, use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "AWS/Route53Resolver"
  ```

**Topics**
+ [CloudWatch metrics for Route 53 Resolver](#cloudwatch-metrics-resolver)
+ [Dimensions for Route 53 Resolver metrics](#cloudwatch-dimensions-resolver)

### CloudWatch metrics for Route 53 Resolver<a name="cloudwatch-metrics-resolver"></a>

`AWS/Route53Resolver` namespace includes metrics for Route 53 Resolver endpoints and for IP addresses\.

**Topics**
+ [Metrics for Resolver endpoints](#cloudwatch-metrics-resolver-endpoint)
+ [Metrics for Resolver IP addresses](#cloudwatch-metrics-resolver-ip-address)

#### Metrics for Resolver endpoints<a name="cloudwatch-metrics-resolver-endpoint"></a>

The `AWS/Route53Resolver` namespace includes the following metrics for Route 53 Resolver endpoints\.

**InboundQueryVolume**  
For inbound endpoints, the number of DNS queries forwarded from your network to your VPCs through the endpoint specified by `EndpointId`\.  
Valid statistics: Sum  
Units: Count

**OutboundQueryVolume**  
For outbound endpoints, the number of DNS queries forwarded from your VPCs to your network through the endpoint specified by `EndpointId`\.  
Valid statistics: Sum  
Units: Count

**OutboundQueryAggregatedVolume**  
For outbound endpoints, the total number of DNS queries forwarded from Amazon VPCs to your network, including the following:  
+ The number of DNS queries forwarded from your VPCs to your network through the endpoint that is specified by `EndpointId`\.
+ When the current account shares Resolver rules with other accounts, queries from VPCs that are created by other accounts that are forwarded to your network through the endpoint that is specified by `EndpointId`\. 
Valid statistics: Sum  
Units: Count

#### Metrics for Resolver IP addresses<a name="cloudwatch-metrics-resolver-ip-address"></a>

The `AWS/Route53Resolver` namespace includes the following metrics for each IP address that's associated with a Resolver inbound or outbound endpoint\. \(When you specify an endpoint, Resolver creates an Amazon VPC [elastic network interface](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html)\.\)

**InboundQueryVolume**  
For each IP address for your inbound endpoints, the number of DNS queries forwarded from your network to the specified IP address\. Each IP address is identified by the IP address ID\. You can get this value using the Route 53 console\. On the page for the applicable endpoint, in the IP addresses section, see the **IP address ID** column\. You can also get the value programmatically using [ListResolverEndpointIpAddresses](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListResolverEndpointIpAddresses.html)\.   
Valid statistics: Sum  
Units: Count

**OutboundQueryAggregatedVolume**  
For each IP address for your outbound endpoints, the total number of DNS queries forwarded from Amazon VPCs to your network, including the following:  
+ The number of DNS queries forwarded from your VPCs to your network using the specified IP address\.
+ When the current account shares Resolver rules with other accounts, queries from VPCs that are created by other accounts that are forwarded to your network through using the specified IP address\. 
Each IP address is identified by the IP address ID\. You can get this value using the Route 53 console\. On the page for the applicable endpoint, in the IP addresses section, see the **IP address ID** column\. You can also get the value programmatically using [ListResolverEndpointIpAddresses](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListResolverEndpointIpAddresses.html)\.   
Valid statistics: Sum  
Units: Count

### Dimensions for Route 53 Resolver metrics<a name="cloudwatch-dimensions-resolver"></a>

Route 53 Resolver metrics for inbound and outbound endpoints use the `AWS/Route53Resolver` namespace and provide metrics for `EndpointId`\. If you specify a value for the `EndpointId` dimension, CloudWatch returns the number of DNS queries for the specified endpoint\. If you don't specify `EndpointId`, CloudWatch returns the number of DNS queries for all endpoints that were created by the current AWS account\.