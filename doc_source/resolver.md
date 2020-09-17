# Resolving DNS queries between VPCs and your network<a name="resolver"></a>

When you create a VPC using Amazon VPC, Route 53 Resolver automatically answers DNS queries for local VPC domain names for EC2 instances \(ec2\-192\-0\-2\-44\.compute\-1\.amazonaws\.com\) and records in private hosted zones \(acme\.example\.com\)\. For all other domain names, Resolver performs recursive lookups against public name servers\.

You also can integrate DNS resolution between Resolver and DNS resolvers on your network by configuring forwarding rules\. *Your network* can include any network that is reachable from your VPC, such as the following:
+ The VPC itself
+ Another peered VPC
+ An on\-premises network that is connected to AWS with AWS Direct Connect, a VPN, or a network address translation \(NAT\) gateway

Before you start to forward queries, you create Resolver inbound and/or outbound endpoints in the connected VPC\. These endpoints provide a path for inbound or outbound queries:

**Inbound endpoint: DNS resolvers on your network can forward DNS queries to Route 53 Resolver via this endpoint**  
This allows your DNS resolvers to easily resolve domain names for AWS resources such as EC2 instances or records in a Route 53 private hosted zone\. For more information, see [How DNS resolvers on your network forward DNS queries to Route 53 Resolver](#resolver-overview-forward-network-to-vpc)\.

**Outbound endpoint: Resolver conditionally forwards queries to resolvers on your network via this endpoint**  
To forward selected queries, you create Resolver rules that specify the domain names for the DNS queries that you want to forward \(such as example\.com\), and the IP addresses of the DNS resolvers on your network that you want to forward the queries to\. If a query matches multiple rules \(example\.com, acme\.example\.com\), Resolver chooses the rule with the most specific match \(acme\.example\.com\) and forwards the query to the IP addresses that you specified in that rule\. For more information, see [How Route 53 Resolver forwards DNS queries from your VPCs to your network](#resolver-overview-forward-vpc-to-network)\. 

Like Amazon VPC, Resolver is regional\. In each region where you have VPCs, you can choose whether to forward queries from your VPCs to your network \(outbound queries\), from your network to your VPCs \(inbound queries\), or both\.

**Note**  
When you create a Resolver endpoint, you can't specify a VPC that has the instance tenancy attribute set to `dedicated`\. For more information, see [Using Resolver in VPCs that are configured for dedicated instance tenancy](#resolver-considerations-dedicated-instance-tenancy)\.

To use inbound or outbound forwarding, you create a Resolver endpoint in your VPC\. As part of the definition of an endpoint, you specify the IP addresses that you want to forward inbound DNS queries to or the IP addresses that you want outbound queries to originate from\. For each IP address that you specify, Resolver automatically creates a VPC elastic network interface\.

The following diagram shows the path of a DNS query from a DNS resolver on your network to Route 53 Resolver\.

![\[Conceptual graphic that shows the path of a DNS query from a DNS resolver on your network to Route 53 Resolver.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/Resolver-inbound-endpoint.png)

The following diagram shows the path of a DNS query from an EC2 instance in one of your VPCs to a DNS resolver on your network\.

![\[Conceptual graphic that shows the path of a DNS query from your network to Route 53 Resolver.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/Resolver-outbound-endpoint.png)

For an overview of VPC network interfaces, see [Elastic network interfaces](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_ElasticNetworkInterfaces.html) in the *Amazon VPC User Guide*\.

**Topics**
+ [How DNS resolvers on your network forward DNS queries to Route 53 Resolver](#resolver-overview-forward-network-to-vpc)
+ [How Route 53 Resolver forwards DNS queries from your VPCs to your network](#resolver-overview-forward-vpc-to-network)
+ [Considerations when creating inbound and outbound endpoints](#resolver-choose-vpc)

## How DNS resolvers on your network forward DNS queries to Route 53 Resolver<a name="resolver-overview-forward-network-to-vpc"></a>

When you want to forward DNS queries from your network to Route 53 Resolver in an AWS Region, you perform the following steps:

1. You create a Route 53 Resolver inbound endpoint in a VPC and specify the IP addresses that the resolvers on your network forward DNS queries to\.

   For each IP address that you specify for the inbound endpoint, Resolver creates a VPC elastic network interface in the VPC where you created the inbound endpoint\. 

1. You configure resolvers on your network to forward DNS queries for the applicable domain names to the IP addresses that you specified in the inbound endpoint\. For more information, see [Considerations when creating inbound and outbound endpoints](#resolver-choose-vpc)\.

Here's how Resolver resolves DNS queries that originate on your network:

1. A web browser or another application on your network submits a DNS query for a domain name that you forwarded to Resolver\.

1. A resolver on your network forwards the query to the IP addresses in your inbound endpoint\.

1. The inbound endpoint forwards the query to Resolver\.

1. Resolver gets the applicable value for the domain name in the DNS query, either internally or by performing a recursive lookup against public name servers\.

1. Resolver returns the value \(typically an IPv4 IP address\) to the inbound endpoint\.

1. The inbound endpoint returns the value to the resolver on your network\.

1. The resolver on your network returns the value to the application\.

1. Using the value that was returned by Resolver, the application submits an HTTP request, for example, a request for an object in an Amazon S3 bucket\.

Creating an inbound endpoint doesn't change the behavior of Resolver, it just provides a path from a location outside the AWS network to Resolver\.

## How Route 53 Resolver forwards DNS queries from your VPCs to your network<a name="resolver-overview-forward-vpc-to-network"></a>

When you want to forward DNS queries from the EC2 instances in one or more VPCs in an AWS Region to your network, you perform the following steps\.

1. You create a Route 53 Resolver outbound endpoint in a VPC, and you specify several values:
   + The VPC that you want DNS queries to pass through on the way to the resolvers on your network\. 
   + The IP addresses in your VPC that you want Resolver to forward DNS queries from\. To hosts on your network, these are the IP addresses that the DNS queries originate from\.
   + A [VPC security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)

   For each IP address that you specify for the outbound endpoint, Resolver creates an Amazon VPC elastic network interface in the VPC that you specify\. For more information, see [Considerations when creating inbound and outbound endpoints](#resolver-choose-vpc)\.

1. You create one or more rules, which specify the domain names of the DNS queries that you want Resolver to forward to resolvers on your network\. You also specify the IP addresses of the resolvers\. For more information, see [Using rules to control which queries are forwarded to your network](#resolver-overview-forward-vpc-to-network-using-rules)\.

1. You associate each rule with the VPCs for which you want to forward DNS queries to your network\.

**Topics**
+ [Using rules to control which queries are forwarded to your network](#resolver-overview-forward-vpc-to-network-using-rules)
+ [How Resolver determines whether the domain name in a query matches any rules](#resolver-overview-forward-vpc-to-network-domain-name-matches)
+ [How Resolver determines where to forward DNS queries](#resolver-overview-forward-vpc-to-network-where-to-forward-queries)
+ [Using rules in multiple Regions](#resolver-overview-forward-vpc-to-network-using-rules-multiple-regions)
+ [Domain names that Resolver creates autodefined system rules for](#resolver-overview-forward-vpc-to-network-autodefined-rules)

### Using rules to control which queries are forwarded to your network<a name="resolver-overview-forward-vpc-to-network-using-rules"></a>

Rules control which DNS queries Route 53 Resolver forwards to DNS resolvers on your network and which queries Resolver answers itself\. 

You can categorize rules in a couple of ways\. One way is by who creates the rules:
+ **Autodefined rules** – Resolver automatically creates autodefined rules and associates the rules with your VPCs\. Most of these rules apply to the AWS\-specific domain names that Resolver answers queries for\. For more information, see [Domain names that Resolver creates autodefined system rules for](#resolver-overview-forward-vpc-to-network-autodefined-rules)\.
+ **Custom rules** – You create custom rules and associate the rules with VPCs\. Currently, you can create only one type of custom rule, conditional forwarding rules, also known as forwarding rules\. Forwarding rules cause Resolver to forward DNS queries from your VPCs to the IP addresses for DNS resolvers on your network\.

  If you create a forwarding rule for the same domain as an autodefined rule, Resolver forwards queries for that domain name to DNS resolvers on your network based on the settings in the forwarding rule\.

Another way to categorize rules is by what they do:
+ **Conditional forwarding rules** – You create conditional forwarding rules \(also known as forwarding rules\) when you want to forward DNS queries for specified domain names to DNS resolvers on your network\.
+ **System rules** – System rules cause Resolver to selectively override the behavior that is defined in a forwarding rule\. When you create a system rule, Resolver resolves DNS queries for specified subdomains that would otherwise be resolved by DNS resolvers on your network\.

  By default, forwarding rules apply to a domain name and all its subdomains\. If you want to forward queries for a domain to a resolver on your network but you don't want to forward queries for some subdomains, you create a system rule for the subdomains\. For example, if you create a forwarding rule for example\.com but you don't want to forward queries for acme\.example\.com, you create a system rule and specify acme\.example\.com for the domain name\.
+ **Recursive rule** – Resolver automatically creates a recursive rule named **Internet Resolver**\. This rule causes Route 53 Resolver to act as a recursive resolver for any domain names that you didn't create custom rules for and that Resolver didn't create autodefined rules for\. For information about how to override this behavior, see "Forwarding All Queries to Your Network" later in this topic\.

You can create custom rules that apply to specific domain names \(yours or most AWS domain names\), to public AWS domains names, or to all domain names\. 

**Forwarding queries for specific domain names to your network**  
To forward queries for a specific domain name, such as example\.com, to your network, you create a rule and specify that domain name\. You also specify the IP addresses of the DNS resolvers on your network that you want to forward the queries to\. You then associate each rule with the VPCs for which you want to forward DNS queries to your network\. For example, you can create separate rules for example\.com, example\.org, and example\.net\. Then you can associate the rules with the VPCs in an AWS Region in any combination\.

**Forwarding queries for amazonaws\.com to your network**  
The domain name amazonaws\.com is the public domain name for AWS resources such as EC2 instances and S3 buckets\. If you want to forward queries for amazonaws\.com to your network, create a rule, specify amazonaws\.com for the domain name, and specify **Forward** for the rule type\.  
Resolver doesn't automatically forward DNS queries for some amazonaws\.com subdomains even if you create a forwarding rule for amazonaws\.com\. For more information, see [Domain names that Resolver creates autodefined system rules for](#resolver-overview-forward-vpc-to-network-autodefined-rules)\. For information about how to override this behavior, see "Forwarding All Queries to Your Network," immediately following\.

**Forwarding all queries to your network**  
If you want to forward all queries to your network, you create a rule, specify "\." \(dot\) for the domain name, and associate the rule with the VPCs for which you want to forward all DNS queries to your network\. Resolver still doesn't forward all DNS queries to your network because using a DNS resolver outside of AWS would break some functionality\. For example, some internal AWS domain names have internal IP address ranges that aren't accessible from outside of AWS\. For a list of the domain names for which queries aren't forwarded to your network when you create a rule for "\.", see [Domain names that Resolver creates autodefined system rules for](#resolver-overview-forward-vpc-to-network-autodefined-rules)\.  
If you want to try forwarding DNS queries for all domain names to your network, including the domain names that are excluded from forwarding by default, you can create a "\." rule and do one of the following:  
+ Set the `enableDnsHostnames` flag for the VPC to `false`
+ Create rules for the domain names that are listed in [Domain names that Resolver creates autodefined system rules for](#resolver-overview-forward-vpc-to-network-autodefined-rules)
If you forward all domain names to your network, including the domain names that Resolver excludes when you create a "\." rule, some features might stop working\.

### How Resolver determines whether the domain name in a query matches any rules<a name="resolver-overview-forward-vpc-to-network-domain-name-matches"></a>

Route 53 Resolver compares the domain name in the DNS query with the domain name in the rules that are associated with the VPC that the query originated from\. Resolver considers the domain names to match in the following cases:
+ The domain names match exactly
+ The domain name in the query is a subdomain of the domain name in the rule

For example, if the domain name in the rule is acme\.example\.com, Resolver considers the following domain names in a DNS query to be a match:
+ acme\.example\.com
+ zenith\.acme\.example\.com

The following domain names are not a match:
+ example\.com
+ nadir\.example\.com

If the domain name in a query matches the domain name in more than one rule \(such as example\.com and www\.example\.com\), Resolver routes outbound DNS queries using the rule that contains the most specific domain name \(www\.example\.com\)\.

### How Resolver determines where to forward DNS queries<a name="resolver-overview-forward-vpc-to-network-where-to-forward-queries"></a>

When an application that runs on an EC2 instance in a VPC submits a DNS query, Route 53 Resolver performs the following steps:

1. Resolver checks for domain names in rules\.

   If the domain name in a query matches the domain name in a rule, Resolver forwards the query to the IP address that you specified when you created the outbound endpoint\. The outbound endpoint then forwards the query to the IP addresses of resolvers on your network, which you specified when you created the rule\.

   For more information, see [How Resolver determines whether the domain name in a query matches any rules](#resolver-overview-forward-vpc-to-network-domain-name-matches)\. 

1. Resolver forwards DNS queries based on the settings in the "\." rule\.

   If the domain name in a query doesn't match the domain name in any other rules, Resolver forwards the query based on the settings in the autodefined "\." \(dot\) rule\. The dot rule applies to all domain names except some AWS internal domain names and record names in private hosted zones\. This rule causes Resolver to forward DNS queries to public name servers if the domain names in queries don't match any names in your custom forwarding rules\. If you want to forward all queries to the DNS resolvers on your network, you can create a custom forwarding rule, specify "\." for the domain name, specify **Forwarding** for **Type**, and specify the IP addresses of those resolvers\. 

1. Resolver returns the response to the application that submitted the query\.

### Using rules in multiple Regions<a name="resolver-overview-forward-vpc-to-network-using-rules-multiple-regions"></a>

Route 53 Resolver is a regional service, so objects that you create in one AWS Region are available only in that Region\. To use the same rule in more than one Region, you must create the rule in each Region\.

The AWS account that created a rule can share the rule with other AWS accounts\. For more information, see [Sharing forwarding rules with other AWS accounts and using shared rules](resolver-rules-managing.md#resolver-rules-managing-sharing)\.

### Domain names that Resolver creates autodefined system rules for<a name="resolver-overview-forward-vpc-to-network-autodefined-rules"></a>

Resolver automatically creates autodefined system rules that define how queries for selected domains are resolved by default:
+ For private hosted zones and for Amazon EC2–specific domain names \(such as compute\.amazonaws\.com and compute\.internal\), autodefined rules ensure that your private hosted zones and EC2 instances continue to resolve if you create conditional forwarding rules for less specific domain names such as "\." \(dot\) or "com"\.
+ For publicly reserved domain names \(such as localhost and 10\.in\-addr\.arpa\), DNS best practices recommend that queries are answered locally instead of being forwarded to public name servers\. See [RFC 6303, Locally Served DNS Zones](https://tools.ietf.org/html/rfc6303)\.

**Note**  
If you create a conditional forwarding rule for "\." \(dot\) or "com", we recommend that you also create a system rule for amazonaws\.com\. \(System rules cause Resolver to locally resolve DNS queries for specific domains and subdomains\.\) Creating this system rule improves performance, reduces the number of queries that are forwarded to your network, and reduces Resolver charges\.

If you want to override an autodefined rule, you can create a conditional forwarding rule for the same domain name\. 

Resolver creates the following autodefined rules\.

**Rules for private hosted zones**  
For each private hosted zone that you associate with a VPC, Resolver creates a rule and associates it with the VPC\. If you associate the private hosted zone with multiple VPCs, Resolver associates the rule with the same VPCs\.  
The rule has a type of **Forward**\.

**Rules for various AWS internal domain names**  
All rules for the internal domain names in this section have a type of **Forward**\. Resolver forwards DNS queries for these domain names to the authoritative name servers for the VPC\.  
Resolver creates most of these rules when you set the `enableDnsHostnames` flag for a VPC to `true`\. Resolver creates the rules even if you aren't using Resolver endpoints\.
Resolver creates the following autodefined rules and associates them with a VPC when you set the `enableDnsHostnames` flag for the VPC to `true`:   
+ *Region\-name*\.compute\.internal, for example, eu\-west\-1\.compute\.internal\. The us\-east\-1 Region doesn't use this domain name\.
+ *Region\-name*\.compute\.*amazon\-domain\-name*, for example, eu\-west\-1\.compute\.amazonaws\.com or cn\-north\-1\.compute\.amazonaws\.com\.cn\. The us\-east\-1 Region doesn't use this domain name\.
+ ec2\.internal\. Only the us\-east\-1 Region uses this domain name\.
+ compute\-1\.internal\. Only the us\-east\-1 Region uses this domain name\.
+ compute\-1\.amazonaws\.com\. Only the us\-east\-1 Region uses this domain name\.
The following autodefined rules are for the reverse DNS lookup for the rules that Resolver creates when you set the `enableDnsHostnames` flag for the VPC to `true`\.  
+ 10\.in\-addr\.arpa
+ 16\.172\.in\-addr\.arpa through 31\.172\.in\-addr\.arpa 
+ 168\.192\.in\-addr\.arpa
+ 254\.169\.254\.169\.in\-addr\.arpa
+ Rules for each of the CIDR ranges for the VPC\. For example, if a VPC that has a CIDR range of 10\.0\.0\.0/23, Resolver creates the following rules: 
  + 0\.0\.10\.in\-addr\.arpa
  + 1\.0\.10\.in\-addr\.arpa
The following autodefined rules, for localhost\-related domains, also are created and associated with a VPC when you set the `enableDnsHostnames` flag for the VPC to `true`:  
+ localhost
+ localdomain
+ 127\.in\-addr\.arpa
+ 1\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.ip6\.arpa
+ 0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.0\.ip6\.arpa
Resolver creates the following autodefined rules and associates them with your VPC when you peer the VPC with another VPC:  
+ The reverse DNS lookup for the peer VPC's IP address ranges, for example, 0\.192\.in\-addr\.arpa

  If you add an IPv4 CIDR block to a VPC, Resolver adds an autodefined rule for the new IP address range\.
+ If the other VPC is in another Region, the following domain names:
  + *Region\-name*\.compute\.internal\. The us\-east\-1 Region doesn't use this domain name\.
  + *Region\-name*\.compute\.*amazon\-domain\-name*\. The us\-east\-1 Region doesn't use this domain name\.
  + ec2\.internal\. Only the us\-east\-1 Region uses this domain name\.
  + compute\-1\.amazonaws\.com\. Only the us\-east\-1 Region uses this domain name\.

**A rule for all other domains**  
Resolver creates a "\." \(dot\) rule that applies to all domain names that aren't specified earlier in this topic\. The "\." rule has a type of **Recursive**, which means that the rule causes Resolver to act as a recursive resolver\.

## Considerations when creating inbound and outbound endpoints<a name="resolver-choose-vpc"></a>

Before you create inbound and outbound Resolver endpoints in an AWS Region, consider the following issues\.

**Topics**
+ [Number of inbound and outbound endpoints in each AWS Region](#resolver-considerations-number-of-endpoints)
+ [Using the same VPC for inbound and outbound endpoints](#resolver-considerations-same-vpc-inbound-outbound)
+ [Inbound endpoints and private hosted zones](#resolver-considerations-inbound-endpoint-private-zone)
+ [VPC peering](#resolver-considerations-vpc-peering)
+ [IP addresses in shared subnets](#resolver-considerations-shared-subnets)
+ [Connection between your network and the VPCs that you create endpoints in](#resolver-considerations-connection-between-network-and-vpcs)
+ [When you share rules, you also share outbound endpoints](#resolver-considerations-share-rules-share-outbound-endpoints)
+ [Using Resolver in VPCs that are configured for dedicated instance tenancy](#resolver-considerations-dedicated-instance-tenancy)

**Number of inbound and outbound endpoints in each AWS Region**  
When you want to integrate DNS for the VPCs in an AWS Region with DNS for your network, you typically need one Resolver inbound endpoint \(for DNS queries that you're forwarding to your VPCs\) and one outbound endpoint \(for queries that you're forwarding from your VPCs to your network\)\. You can create multiple inbound endpoints and multiple outbound endpoints, but one endpoint is sufficient to handle the DNS queries in either direction\. Note the following:  
+ For each Resolver endpoint, you specify two or more IP addresses in different Availability Zones\. Each IP address in an endpoint can handle a large number of DNS queries per second\. \(For the current maximum number of queries per second per IP address in an endpoint, see [Quotas on Route 53 Resolver](DNSLimitations.md#limits-api-entities-resolver)\.\) If you need Resolver to handle more queries, you can add more IP addresses to your existing endpoint instead of adding another endpoint\.
+ Resolver pricing is based on the number of IP addresses in your endpoints and on the number of DNS queries that the endpoint processes\. Each endpoint includes a minimum of two IP addresses\. For more information about Resolver pricing, see [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.
+ Each rule specifies the outbound endpoint that DNS queries are forwarded from\. If you create multiple outbound endpoints in an AWS Region and you want to associate some or all Resolver rules with every VPC, you need to create multiple copies of those rules\.

**Using the same VPC for inbound and outbound endpoints**  
You can create inbound and outbound endpoints in the same VPC or in different VPCs in the same Region\.

**Inbound endpoints and private hosted zones**  
If you want Resolver to resolve inbound DNS queries using records in a private hosted zone, associate the private hosted zone with the VPC that you created the inbound endpoint in\. For information about associating private hosted zones with VPCs, see [Working with private hosted zones](hosted-zones-private.md)\.

**VPC peering**  
You can use any VPC in an AWS Region for an inbound or an outbound endpoint regardless of whether the VPC that you choose is peered with other VPCs\. For more information, see [Amazon Virtual Private Cloud VPC peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)\.

**IP addresses in shared subnets**  
When you create an inbound or outbound endpoint, you can specify an IP address in a shared subnet only if the current account created the VPC\. If another account creates a VPC and shares a subnet in the VPC with your account, you can't specify an IP address in that subnet\. For more information about shared subnets, see [Working with shared VPCs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html) in the *Amazon VPC User Guide*\.

**Connection between your network and the VPCs that you create endpoints in**  
You must have one of the following connections between your network and the VPCs that you create endpoints in:  
+ **Inbound endpoints** – You must set up either an [AWS Direct Connect](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html) connection or a [VPN connection](https://docs.aws.amazon.com/vpc/latest/userguide/vpn-connections.html) between your network and each VPC that you create an inbound endpoint for\.
+ **Outbound endpoints** – You must set up an [AWS Direct Connect](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html) connection, a [VPN connection](https://docs.aws.amazon.com/vpc/latest/userguide/vpn-connections.html), or a [network address translation \(NAT\) gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) between your network and each VPC that you create an outbound endpoint for\.

**When you share rules, you also share outbound endpoints**  
When you create a rule, you specify the outbound endpoint that you want Resolver to use to forward DNS queries to your network\. If you share the rule with another AWS account, you also indirectly share the outbound endpoint that you specify in the rule\. If you used more than one AWS account to create VPCs in an AWS Region, you can do the following:  
+ Create one outbound endpoint in the Region\.
+ Create rules using one AWS account\.
+ Share the rules with all the AWS accounts that created VPCs in the Region\.
This allows you to use one outbound endpoint in a Region to forward DNS queries to your network from multiple VPCs even if the VPCs were created using different AWS accounts\.

**Using Resolver in VPCs that are configured for dedicated instance tenancy**  
When you create a Resolver endpoint, you can't specify a VPC that has the [instance tenancy attribute](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html) set to `dedicated`\. Resolver doesn't run on single\-tenant hardware\.  
You can still use Resolver to resolve DNS queries that originate in a VPC\. Create at least one VPC that has the instance tenancy attribute set to `default`, and specify that VPC when you create inbound and outbound endpoints\.  
When you create a forwarding rule, you can associate it with any VPC, regardless of the setting for the instance tenancy attribute\.