# Monitoring Route 53 Resolver DNS Firewall rule groups with Amazon CloudWatch<a name="monitoring-resolver-dns-firewall-with-cloudwatch"></a>

You can use Amazon CloudWatch to monitor the number of DNS queries that are filtered by Route 53 Resolver DNS Firewall rule groups\. Amazon CloudWatch collects and processes raw data into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your resources are performing\. By default, metric data for DNS Firewall rule groups is automatically sent to CloudWatch at five\-minute intervals\.

For more information about DNS Firewall, see [Route 53 Resolver DNS Firewall](resolver-dns-firewall.md)\. For more information about CloudWatch, see [What is Amazon CloudWatch?](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

## Metrics and dimensions for Route 53 Resolver DNS Firewall<a name="metrics-dimensions-resolver-dns-firewall"></a>

When you associate a Route 53 Resolver DNS Firewall rule group with a VPC to filter DNS queries, DNS Firewall starts to send metrics and dimensions once every 5 minutes to CloudWatch about the queries that it filters\. For information about the metrics and dimensions for DNS Firewall, see [CloudWatch metrics for Route 53 Resolver DNS Firewall](#cloudwatch-metrics-resolver-dns-firewall)\. 

You can use the following procedures to view the metrics in the CloudWatch console or view them by using the AWS Command Line Interface \(AWS CLI\)\.

**To view DNS Firewall metrics using the CloudWatch console**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. On the navigation bar, choose the Region that you want to view\.

1. In the navigation pane, choose **Metrics**\.

1. On the **All metrics** tab, choose **Route 53 Resolver**\.

1. Choose a metric that you're interested in\. 

**To view metrics using the AWS CLI**
+ At a command prompt, use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "AWS/Route53Resolver"
  ```

**Topics**
+ [CloudWatch metrics for Route 53 Resolver DNS Firewall](#cloudwatch-metrics-resolver-dns-firewall)

### CloudWatch metrics for Route 53 Resolver DNS Firewall<a name="cloudwatch-metrics-resolver-dns-firewall"></a>

The `AWS/Route53Resolver` namespace includes metrics for Route 53 Resolver DNS Firewall rule groups\.

**Topics**
+ [Metrics for Route 53 Resolver DNS Firewall rule groups](#cloudwatch-metrics-resolver-dns-firewall-rule-group)
+ [Metrics for VPCs](#cloudwatch-metrics-resolver-vpc)
+ [Metrics for firewall rule group and VPC association](#cloudwatch-metrics-resolver-firewall-vpc)
+ [Metrics for a domain list in a firewall rule group](#cloudwatch-metrics-domain-list-firewall)

#### Metrics for Route 53 Resolver DNS Firewall rule groups<a name="cloudwatch-metrics-resolver-dns-firewall-rule-group"></a>

**FirewallRuleGroupQueryVolume**  
The number of DNS Firewall queries that match a firewall rule group \(specified by `FirewallRuleGroupId`\)\.  
Dimensions: `FirewallRuleGroupId`  
Valid statistics: Sum  
Units: Count

#### Metrics for VPCs<a name="cloudwatch-metrics-resolver-vpc"></a>

**VPCFirewallQueryVolume**  
The number of DNS Firewall queries from a VPC \(specified by `VpcId`\)\.  
Dimensions: `VpcId`  
Valid statistics: Sum  
Units: Count

#### Metrics for firewall rule group and VPC association<a name="cloudwatch-metrics-resolver-firewall-vpc"></a>

**FirewallRuleGroupVpcQueryVolume**  
The number of DNS Firewall queries from a VPC \(specified by `VpcId`\) that match a firewall rule group \(specified by `FirewallRuleGroupId`\)\.  
Dimensions: `FirewallRuleGroupId, VpcId`  
Valid statistics: Sum  
Units: Count

#### Metrics for a domain list in a firewall rule group<a name="cloudwatch-metrics-domain-list-firewall"></a>

**FirewallRuleGroupVpcQueryVolume**  
The number of DNS firewall queries that match a firewall domain list \(specified by `FirewallDomainListId`\) within a firewall rule group \(specified by `FirewallRuleGroupId`\)\.  
Dimensions: `FirewallRuleGroupId, FirewallDomainListId`  
Valid statistics: Sum  
Units: Count