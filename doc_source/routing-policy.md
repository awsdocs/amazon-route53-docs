# Choosing a routing policy<a name="routing-policy"></a>

When you create a record, you choose a routing policy, which determines how Amazon Route 53 responds to queries: 
+ **Simple routing policy** – Use for a single resource that performs a given function for your domain, for example, a web server that serves content for the example\.com website\. You can use simple routing to create records in a private hosted zone\.
+ **Failover routing policy** – Use when you want to configure active\-passive failover\. You can use failover routing to create records in a private hosted zone\.
+ **Geolocation routing policy** – Use when you want to route traffic based on the location of your users\. You can use geolocation routing to create records in a private hosted zone\.
+ **Geoproximity routing policy** – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another\.
+ **Latency routing policy** – Use when you have resources in multiple AWS Regions and you want to route traffic to the region that provides the best latency\. You can use latency routing to create records in a private hosted zone\.
+ **IP\-based routing policy** – Use when you want to route traffic based on the location of your users, and have the IP addresses that the traffic originates from\.
+ **Multivalue answer routing policy** – Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random\. You can use multivalue answer routing to create records in a private hosted zone\.
+ **Weighted routing policy** – Use to route traffic to multiple resources in proportions that you specify\. You can use weighted routing to create records in a private hosted zone\.

**Topics**
+ [Simple routing](routing-policy-simple.md)
+ [Failover routing](routing-policy-failover.md)
+ [Geolocation routing](routing-policy-geo.md)
+ [Geoproximity routing \(traffic flow only\)](routing-policy-geoproximity.md)
+ [Latency\-based routing](routing-policy-latency.md)
+ [IP\-based routing](routing-policy-ipbased.md)
+ [Multivalue answer routing](routing-policy-multivalue.md)
+ [Weighted routing](routing-policy-weighted.md)
+ [How Amazon Route 53 uses EDNS0 to estimate the location of a user](routing-policy-edns0.md)