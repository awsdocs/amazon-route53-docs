# Creating Records by Using the Amazon Route 53 Console<a name="resource-record-sets-creating"></a>

The following procedure explains how to create records using the Amazon Route 53 console\. For information about how to create records using the Route 53 API, see [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

**Note**  
To create records for complex routing configurations, you can also use the traffic flow visual editor and save the configuration as a traffic policy\. You can then associate the traffic policy with one or more domain names \(such as example\.com\) or subdomain names \(such as www\.example\.com\), in the same hosted zone or in multiple hosted zones\. In addition, you can roll back the updates if the new configuration isn't performing as you expected it to\. For more information, see [Using Traffic Flow to Route DNS Traffic](traffic-flow.md)\.

**To create a record using the Route 53 console**

1. If you're not creating an alias record, go to step 2\. 

   Also go to step 2 if you're creating an alias record that routes DNS traffic to a CloudFront distribution, an Elastic Beanstalk environment, an Amazon S3 bucket, or another Route 53 record\.

   If you're creating an alias record that routes traffic to an Elastic Load Balancing Classic, Application, or Network Load Balancer, and if you created your Route 53 hosted zone and your load balancer using different accounts, perform the procedure [Getting the DNS Name for an ELB Load Balancer](#resource-record-sets-elb-dns-name-procedure) to get the DNS name for the load balancer\. 

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you already have a hosted zone for your domain, skip to step 4\. If you don't, perform the following steps: 

   1. Click **Create Hosted Zone**\.

   1. For **Domain Name**, enter the name of your domain\.

   1. *Optional:* For **Comment**, enter a comment about the hosted zone\.

   1. Click **Create**\.

1. On the **Hosted Zones** page, choose the name of the hosted zone in which you want to create records\.

1. Click **Create Record Set**\.

1. Enter the applicable values\. For more information, see the topic for the kind of record that you want to create:

   + [Values for Basic Records](resource-record-sets-values-basic.md)

   + [Values for Alias Records](resource-record-sets-values-alias.md)

   + [Values for Failover Records](resource-record-sets-values-failover.md)

   + [Values for Failover Alias Records](resource-record-sets-values-failover-alias.md)

   + [Values for Geolocation Records](resource-record-sets-values-geo.md)

   + [Values for Geolocation Alias Records](resource-record-sets-values-geo-alias.md)

   + [Values for Latency Records](resource-record-sets-values-latency.md)

   + [Values for Latency Alias Records](resource-record-sets-values-latency-alias.md)

   + [Values for Multivalue Answer Records](resource-record-sets-values-multivalue.md)

   + [Values for Weighted Records](resource-record-sets-values-weighted.md)

   + [Values for Weighted Alias Records](resource-record-sets-values-weighted-alias.md)

1. Click **Create**\.
**Note**  
Your new records take time to propagate to the Route 53 DNS servers\. Currently, the only way to verify that changes have propagated is to use the [GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API action\. Changes generally propagate to all Route 53 name servers within 60 seconds\.

1. If you're creating multiple records, repeat steps 5 through 7\.

**Getting the DNS Name for an ELB Load Balancer**

1. Sign in to the AWS Management Console using the AWS account that was used to create the Classic, Application, or Network Load Balancer that you want to create an alias record for\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, click **Load Balancers**\.

1. In the list of load balancers, select the load balancer for which you want to create an alias record\.

1. On the **Description** tab, get the value of **DNS name**\.

1. If you want to create alias records for other ELB load balancers, repeat steps 4 and 5\. 

1. Sign out of the AWS Management Console\.

1. Sign in to the AWS Management Console again using the AWS account that you used to create the Route 53 hosted zone\.

1. Return to step 3 of the procedure [Creating Records by Using the Amazon Route 53 Console](#resource-record-sets-creating)\.