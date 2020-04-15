# Using latency and weighted records in Amazon Route 53 to route traffic to multiple Amazon EC2 instances in a Region<a name="TutorialLBRMultipleEC2InRegion"></a>

If your application is running on Amazon EC2 instances in two or more Amazon EC2 regions, and if you have more than one Amazon EC2 instance in one or more regions, you can use latency\-based routing to route traffic to the correct region and then use weighted records to route traffic to instances within the region based on weights that you specify\. 

For example, suppose you have three Amazon EC2 instances with Elastic IP addresses in the US East \(Ohio\) region and you want to distribute requests across all three IPs evenly for users for whom US East \(Ohio\) is the appropriate region\. Just one Amazon EC2 instance is sufficient in the other regions, although you can apply the same technique to many regions at once\.<a name="TutorialLBRMultipleEC2InRegionProcedure"></a>

**To use latency and weighted records in Amazon Route 53 to route traffic to multiple Amazon EC2 instances in a region**

1. Create a group of weighted records for the Amazon EC2 instances in the region\. Note the following:
   + Give each weighted record the same value for **Name** \(for example, `us-east.example.com`\) and **Type**\. 
   + For **Value**, specify the value of one of the Elastic IP addresses\. 
   + If you want to weight the Amazon EC2 instances equally, specify the same value for **Weight**\.
   + Specify a unique value for **Set ID** for each record\.

1. If you have multiple Amazon EC2 instances in other regions, repeat Step 1 for the other regions\. Specify a different value for **Name** in each region\.

1. For each region in which you have multiple Amazon EC2 instances \(for example, US East \(Ohio\)\), create a latency alias record\. For the value of **Alias Target**, specify the value of the **Name** field \(for example, `us-east.example.com`\) that you assigned to the weighted records in that region\. 

1. For each region in which you have one Amazon EC2 instance, create a latency record\. For the value of **Name**, specify the same value that you specified for the latency alias records that you created in Step 3\. For **Value**, specify the Elastic IP address of the Amazon EC2 instance in that region\.

For more information about creating records, see [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)\.