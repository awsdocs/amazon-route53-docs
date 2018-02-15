# Configuring DNS Failover<a name="dns-failover-configuring"></a>

When you have more than one resource performing the same function—for example, more than one HTTP server or mail server—you can configure Amazon Route 53 to check the health of your resources and respond to DNS queries using only the healthy resources\. For example, suppose your website, example\.com, is hosted on 10 servers, two each in five data centers around the world\. You can configure Route 53 to check the health of those servers and to respond to DNS queries for example\.com using only the servers that are currently healthy\.

You can set up a variety of failover configurations using Route 53 alias, failover, geolocation, geoproximity, latency, multivalue, and weighted records:

+ **Active\-active failover:** Use this failover configuration when you want all of your resources to be available the majority of the time\. When a resource becomes unavailable, Route 53 can detect that it's unhealthy and stop including it when responding to queries\.

+ **Active\-passive failover:** Use this failover configuration when you want a primary group of resources to be available the majority of the time and you want a secondary group of resources to be on standby in case all of the primary resources become unavailable\. When responding to queries, Route 53 includes only the healthy primary resources\. If all of the primary resources are unhealthy, Route 53 begins to include only the healthy secondary resources in response to DNS queries\.

+ **Active\-active\-passive and other mixed configurations:** You can combine alias and non\-alias records to produce a variety of Route 53 behaviors\.

Route 53 can check the health of your resources in both simple and complex configurations:

+ In all configurations, you create a group of records that all have the same name and type, for example, a group of weighted records for example\.com for which the type is A\. You then configure Route 53 to check the health of the corresponding resources\. Route 53 responds to DNS queries based on the health of your resources\. For more information, see [How Health Checks Work in Simple Amazon Route 53 Configurations](dns-failover-simple-configs.md)\.

+ In more complex configurations, you use a combination of alias records, such as weighted alias and failover alias records, to create a tree of records\. As with a simple configuration, you configure Route 53 to check the health of your resources\. However, you can also configure the alias records to respond to the status of alias targets and to skip to another branch in the tree if all of the alias targets in one branch are unhealthy\. Complex configurations give you more control over how Route 53 responds to your requests\. For example, you might use latency\-based routing to select a region close to a user and use an ELB Classic, Application, or Network Load Balancer within each region to protect against the failure of a single endpoint or an availability zone\. For more information, see [How Health Checks Work in Complex Amazon Route 53 Configurations](dns-failover-complex-configs.md)\.