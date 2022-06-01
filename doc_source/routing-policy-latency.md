# Latency\-based routing<a name="routing-policy-latency"></a>

If your application is hosted in multiple AWS Regions, you can improve performance for your users by serving their requests from the AWS Region that provides the lowest latency\. 

**Note**  
Data about the latency between users and your resources is based entirely on traffic between users and AWS data centers\. If you aren't using resources in an AWS Region, the actual latency between your users and your resources can vary significantly from AWS latency data\. This is true even if your resources are located in the same city as an AWS Region\.

To use latency\-based routing, you create latency records for your resources in multiple AWS Regions\. When Route 53 receives a DNS query for your domain or subdomain \(example\.com or acme\.example\.com\), it determines which AWS Regions you've created latency records for, determines which region gives the user the lowest latency, and then selects a latency record for that region\. Route 53 responds with the value from the selected record, such as the IP address for a web server\. 

For example, suppose you have ELB load balancers in the US West \(Oregon\) Region and in the Asia Pacific \(Singapore\) Region\. You created a latency record for each load balancer\. Here's what happens when a user in London enters the name of your domain in a browser:

1. DNS routes the query to a Route 53 name server\.

1. Route 53 refers to its data on latency between London and the Singapore region and between London and the Oregon region\. 

1. If latency is lower between the London and Oregon regions, Route 53 responds to the query with the IP address for the Oregon load balancer\. If latency is lower between London and the Singapore region, Route 53 responds with the IP address for the Singapore load balancer\. 

Latency between hosts on the internet can change over time as a result of changes in network connectivity and routing\. Latency\-based routing is based on latency measurements performed over a period of time, and the measurements reflect these changes\. A request that is routed to the Oregon region this week might be routed to the Singapore region next week\.

**Note**  
When a browser or other viewer uses a DNS resolver that supports the edns\-client\-subnet extension of EDNS0, the DNS resolver sends Route 53 a truncated version of the user's IP address\. If you configure latency\-based routing, Route 53 considers this value when routing traffic to your resources\. For more information, see [How Amazon Route 53 uses EDNS0 to estimate the location of a user](routing-policy-edns0.md)\.

For information about values that you specify when you use the latency routing policy to create records, see the following topics:
+ [Values specific for latency records](resource-record-sets-values-latency.md)
+ [Values specific for latency alias records](resource-record-sets-values-latency-alias.md)
+ [Values that are common for all routing policies](resource-record-sets-values-shared.md)
+ [Values that are common for alias records for all routing policies](resource-record-sets-values-alias-common.md)