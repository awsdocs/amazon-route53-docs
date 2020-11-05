# Configure an outbound endpoint<a name="resolver-outbound-endpoint"></a>

An outbound endpoint determines the VPC that queries pass through and the IP addresses in the VPC that Route 53 Resolver forwards queries to on their way to your network\. You can use the same outbound endpoint for multiple VPCs in the same AWS Region, or you can create multiple outbound endpoints\. For each outbound endpoint, you need either an AWS Direct Connect connection to your network or a VPC connection\. 

When you configure an outbound endpoint, you specify settings for a VPC elastic network interface that Resolver creates for you automatically in the VPC and AWS Region that you specify\. DNS queries pass from VPCs in a specified Region through the network interface to resolvers in your network\.

After you create an outbound endpoint, you must create one or more rules and associate them with one or more VPCs\. Rules specify the domain names of the DNS queries that you want to forward to your network\. 

## Learn more<a name="resolver-outbound-endpoint-learn-more"></a>
+ [How Resolver Forwards DNS Queries from Your VPCs to Your Network](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html#resolver-overview-forward-vpc-to-network)
+ [Forwarding outbound DNS queries to your network](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-forwarding-outbound-queries.html)