# Creating records by using the Amazon Route 53 console<a name="resource-record-sets-creating"></a>

The following procedure explains how to create records using the Amazon Route 53 console\. For information about how to create records using the Route 53 API, see [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

**Note**  
To create records for complex routing configurations, you can also use the traffic flow visual editor and save the configuration as a traffic policy\. You can then associate the traffic policy with one or more domain names \(such as example\.com\) or subdomain names \(such as www\.example\.com\), in the same hosted zone or in multiple hosted zones\. In addition, you can roll back the updates if the new configuration isn't performing as you expected it to\. For more information, see [Using traffic flow to route DNS traffic](traffic-flow.md)\.<a name="resource-record-sets-creating-procedure"></a>

**To create a record using the Route 53 console**

1. If you're not creating an alias record, go to step 2\. 

   Also go to step 2 if you're creating an alias record that routes DNS traffic to an AWS resource other than an Elastic Load Balancing load balancer or another Route 53 record\.

   If you're creating an alias record that routes traffic to an ELB load balancer, and if you created your hosted zone and your load balancer using different accounts, perform the procedure [Getting the DNS name for an ELB load balancer](#resource-record-sets-elb-dns-name-procedure) to get the DNS name for the load balancer\. 

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. If you already have a hosted zone for your domain, skip to step 5\. If you don't, perform the applicable procedure to create a hosted zone:
   + To route internet traffic to your resources, such as Amazon S3 buckets or Amazon EC2 instances, see [Creating a public hosted zone](CreatingHostedZone.md)\.
   + To route traffic in your VPC, see [Creating a private hosted zone](hosted-zone-private-creating.md)\.

1. On the **Hosted Zones** page, choose the name of the hosted zone that you want to create records in\.

1. Choose **Create Record Set**\.

1. Enter the applicable values\. For more information, see the topic for the kind of record that you want to create:
   + [Values for basic records](resource-record-sets-values-basic.md)
   + [Values for alias records](resource-record-sets-values-alias.md)
   + [Values for failover records](resource-record-sets-values-failover.md)
   + [Values for failover alias records](resource-record-sets-values-failover-alias.md)
   + [Values for geolocation records](resource-record-sets-values-geo.md)
   + [Values for geolocation alias records](resource-record-sets-values-geo-alias.md)
   + [Values for latency records](resource-record-sets-values-latency.md)
   + [Values for latency alias records](resource-record-sets-values-latency-alias.md)
   + [Values for multivalue answer records](resource-record-sets-values-multivalue.md)
   + [Values for weighted records](resource-record-sets-values-weighted.md)
   + [Values for weighted alias records](resource-record-sets-values-weighted-alias.md)

1. Choose **Create**\.
**Note**  
Your new records take time to propagate to the Route 53 DNS servers\. Currently, the only way to verify that changes have propagated is to use the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API action\. Changes generally propagate to all Route 53 name servers within 60 seconds\.

1. If you're creating multiple records, repeat steps 6 through 8\.<a name="resource-record-sets-elb-dns-name-procedure"></a>

**Getting the DNS name for an ELB load balancer**

1. Sign in to the AWS Management Console using the AWS account that was used to create the Classic, Application, or Network Load Balancer that you want to create an alias record for\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Load Balancers**\.

1. In the list of load balancers, select the load balancer for which you want to create an alias record\.

1. On the **Description** tab, get the value of **DNS name**\.

1. If you want to create alias records for other ELB load balancers, repeat steps 4 and 5\. 

1. Sign out of the AWS Management Console\.

1. Sign in to the AWS Management Console again using the AWS account that you used to create the Route 53 hosted zone\.

1. Return to step 3 of the procedure [Creating records by using the Amazon Route 53 console](#resource-record-sets-creating)\.