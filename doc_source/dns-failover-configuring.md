# Configuring DNS Failover<a name="dns-failover-configuring"></a>

When you have more than one resource performing the same function—for example, more than one HTTP server or mail server—you can configure Amazon Route 53 to check the health of your resources and respond to DNS queries using only the healthy resources\. For example, suppose your website, example\.com, is hosted on six servers, two each in three data centers around the world\. You can configure Route 53 to check the health of those servers and to respond to DNS queries for example\.com using only the servers that are currently healthy\.

Route 53 can check the health of your resources in both simple and complex configurations:

+ In simple configurations, you create a group of records that all have the same name and type, such as a group of weighted records with a type of A for example\.com\. You then configure Route 53 to check the health of the corresponding resources\. Route 53 responds to DNS queries based on the health of your resources\. For more information, see [How Health Checks Work in Simple Amazon Route 53 ConfigurationsHow Health Checks Work in Simple Configurations](dns-failover-simple-configs.md)\.

+ In more complex configurations, you create a tree of records that route traffic based on multiple criteria\. For example, if latency for your users is your most important criterion, then you might use latency alias records to route traffic to the region that provides the best latency\. The latency alias records might have weighted records in each region as the alias target\. The weighted records might route traffic to EC2 instances based on the instance type\. As with a simple configuration, you can configure Route 53 to route traffic based on the health of your resources\. For more information, see [How Health Checks Work in Complex Amazon Route 53 ConfigurationsHow Health Checks Work in Complex Configurations](dns-failover-complex-configs.md)\.


+ [Task List for Configuring DNS Failover](dns-failover-how-to.md)
+ [How Health Checks Work in Simple Amazon Route 53 Configurations](dns-failover-simple-configs.md)
+ [How Health Checks Work in Complex Amazon Route 53 Configurations](dns-failover-complex-configs.md)
+ [How Amazon Route 53 Chooses Records When Health Checking Is Configured](health-checks-how-route-53-chooses-records.md)
+ [Active\-Active and Active\-Passive Failover](dns-failover-types.md)
+ [Configuring Failover in a Private Hosted Zone](dns-failover-private-hosted-zones.md)
+ [How Amazon Route 53 Averts Failover Problems](dns-failover-problems.md)