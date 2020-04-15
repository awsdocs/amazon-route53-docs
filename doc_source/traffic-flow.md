# Using traffic flow to route DNS traffic<a name="traffic-flow"></a>

If you use multiple resources, such as web servers, in multiple locations, it can be a challenge to create records for a complex configuration that uses a combination of Amazon Route 53 routing policies—failover, geolocation, latency, multivalue answer, and weighted\. You can create records one at a time, but it's hard to keep track of the relationships among the records when you're reviewing the settings in a table in the console\.

If you're using the Route 53 console, Route 53 traffic flow provides a visual editor that helps you create complex trees in a fraction of the time with a fraction of the effort\. You can save the configuration as a *traffic policy* and then associate the traffic policy with one or more domain names \(such as example\.com\) or subdomain names \(such as www\.example\.com\), in the same hosted zone or in multiple hosted zones\. \(You can only use traffic flow to create configurations for public hosted zones\.\) You can also use the visual editor to quickly find resources that you need to update and apply the updates to one or more DNS names such as www\.example\.com\. In addition, you can roll back the updates if the new configuration isn't performing as you expected it to\.

For example, using the traffic flow visual editor, you can easily create a configuration in which you use geolocation routing to route all users from one country to a single endpoint and then use latency routing to route all other users to AWS Regions based on the latency between your users and those regions\. You might also use failover routing to route users to a primary ELB load balancer within each region when the load balancer is functioning or to a secondary load balancer when the primary load balancer is unhealthy or is offline for maintenance\.

Here's an overview of how traffic flow works:

1. You use the visual editor to create a traffic policy\. A traffic policy includes information about the routing configuration that you want to create: the routing policies that you want to use and the resources that you want to route DNS traffic to, such as the IP address of each EC2 instance and the domain name of each ELB load balancer\. You can also associate health checks with your endpoints so that Route 53 routes traffic only to healthy resources\. \(Traffic flow also lets you route traffic to non\-AWS resources\.\)

1. You create a *policy record*\. This is where you specify the hosted zone \(such as example\.com\) in which you want to create the configuration that you defined in your traffic policy\. It's also where you specify the DNS name \(such as www\.example\.com\) that you want to associate the configuration with\. You can create more than one policy record in the same hosted zone or in different hosted zones by using the same traffic policy\.

   When you create a policy record, Route 53 creates a tree of records\. The root record appears in the list of records for your hosted zone\. The root record has the DNS name that you specified when you created the policy record\. Route 53 also creates records for the entire rest of the tree, but it hides them from the list of records for your hosted zone\.

1. When a user browses to www\.example\.com, Route 53 responds to the query based on the configuration in the traffic policy that you used to create the policy record\.

**Topics**
+ [Creating and managing traffic policies](traffic-policies.md)
+ [Creating and managing policy records](traffic-policy-records.md)