# IP addresses<a name="resolver-outbound-endpoint-ip-addresses"></a>

Specify the IP addresses in your VPC that you want Route 53 Resolver to forward DNS queries to on the way to resolvers on your network\. These are not the IP addresses of the DNS resolvers on your network; you specify those IP addresses when you create the rules that you associate with one or more VPCs\. 

**Important**  
To improve reliability, we recommend that you specify IP addresses in at least two Availability Zones\. You can optionally specify additional IP addresses in those or other Availability Zones\.

## Learn more<a name="resolver-outbound-endpoint-ip-addresses-learn-more"></a>
+ [Forwarding outbound DNS queries to your network](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-forwarding-outbound-queries.html)