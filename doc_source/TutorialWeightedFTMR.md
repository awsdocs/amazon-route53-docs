# Weighting fault\-tolerant multi\-record answers in Amazon Route 53<a name="TutorialWeightedFTMR"></a>

**Note**  
Records that use the multivalue answer routing policy behave in much the same way as the configuration that is documented in this tutorial\. The main difference is that the tutorial configuration lets you specify weights, which can be useful when your endpoints have different capacities\. For more information, see [Multivalue answer routing](routing-policy.md#routing-policy-multivalue)\.

An Amazon Route 53 weighted record can only be associated with one record, meaning a combination of one name \(for example, `example.com`\) and one record type \(for example, A\)\. But it is often desirable to weight DNS responses that contain multiple records\. 

For example, you might have eight Amazon EC2 instances or Elastic IP endpoints for a service\. If the clients of that service support connection retries \(as all common browsers do\), then providing multiple IP addresses in DNS responses provides those clients with alternative endpoints in the event of the failure of any particular endpoint\. You can even protect against the failure of an availability zone if you configure responses to contain a mix of IPs hosted in two or more availability zones\.

Multi\-record answers are also useful when a large number of clients \(for example, mobile web applications\) share a small set of DNS caches\. In this case, multi\-record answers allow clients to direct requests to several endpoints even if they receive a common DNS response from the shared cache\.

These types of weighted multi\-record answers can be achieved by using a combination of records and weighted alias records\. You can group eight endpoints into two distinct record sets containing four IP addresses each:

`endpoint-a.example.com`, type A, with the following values:
+ 192\.0\.2\.1
+ 192\.0\.2\.2
+ 192\.0\.2\.128
+ 192\.0\.2\.129

`endpoint-b.example.com`, type A, with the following values:
+ 192\.0\.2\.3
+ 192\.0\.2\.4
+ 192\.0\.2\.130
+ 192\.0\.2\.131

You can then create a weighted alias record that points to each group:
+ `www.example.com` aliases to `endpoint-a.example.com`, type A, weight 1
+ `www.example.com` aliases to `endpoint-b.example.com`, type A, weight 1

For more information about creating records, see [Working with records](rrsets-working-with.md)\.