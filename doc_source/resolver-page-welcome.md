# Welcome<a name="resolver-page-welcome"></a>

When you create a VPC using Amazon VPC, you automatically get DNS resolution within the VPC from Route 53 Resolver\. By default, Resolver answers DNS queries for VPC domain names such as domain names for EC2 instances or ELB load balancers\. Resolver performs recursive lookups against public name servers for all other domain names\. 

You can also configure DNS resolution between your VPC and your network over a Direct Connect or VPN connection: 
+ **Forward DNS queries from resolvers on your network to Route 53 Resolver**: DNS resolvers on your network can forward DNS queries to Resolver in a specified VPC\. This allows your DNS resolvers to easily resolve domain names for AWS resources such as EC2 instances or records in a Route 53 private hosted zone\.
+ **Conditionally forward queries from a VPC to resolvers on your network**: You can configure Resolver to forward queries that it receives from EC2 instances in your VPCs to DNS resolvers on your network\. To forward selected queries, you create Resolver rules that specify the domain names for the DNS queries that you want to forward \(such as example\.com\), and the IP addresses of the DNS resolvers on your network that you want to forward the queries to\. If a query matches multiple rules \(example\.com, acme\.example\.com\), Resolver chooses the rule with the most specific match \(acme\.example\.com\) and forwards the query to the IP addresses that you specified in that rule\. 

## Learn more<a name="resolver-page-welcome-learn-more"></a>
+ [How DNS resolvers on your network forward DNS queries to Route 53 Resolver](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html#resolver-overview-forward-network-to-vpc)
+ [How Route 53 Resolver forwards DNS queries from your VPCs to your network](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver.html#resolver-overview-forward-vpc-to-network)