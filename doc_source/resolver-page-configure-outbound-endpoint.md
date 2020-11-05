# Configure outbound endpoint<a name="resolver-page-configure-outbound-endpoint"></a>

To forward DNS queries that originate on Amazon EC2 instances in one or more VPCs to your network, you create an outbound endpoint and one or more rules\.

An outbound endpoint determines the VPC that queries pass through and the IP addresses in the VPC that Route 53 Resolver forwards queries to on their way to your network\. You can use the same outbound endpoint for multiple VPCs in the same Region, or you can create multiple outbound endpoints\. For each outbound endpoint, you need either an AWS Direct Connect connection to your network or a VPC connection\.

## Learn more<a name="resolver-page-configure-outbound-endpoint-learn-more"></a>
+ [Forwarding outbound DNS Queries to your network](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-forwarding-outbound-queries.html)