# Forwarding outbound DNS queries to your network<a name="resolver-forwarding-outbound-queries"></a>

To forward DNS queries that originate on Amazon EC2 instances in one or more VPCs to your network, you create an outbound endpoint and one or more rules:

**Outbound endpoint**  
To forward DNS queries from your VPCs to your network, you create an outbound endpoint\. An outbound endpoint specifies the IP addresses that queries originate from\. Those IP addresses, which you choose from the range of IP addresses available to your VPC, aren't public IP addresses\. This means that, for each outbound endpoint, you need to connect your VPC to your network using AWS Direct Connect connection, a VPC connection, or a network address translation \(NAT\) gateway\. Note that you can use the same outbound endpoint for multiple VPCs in the same Region, or you can create multiple outbound endpoints\.

**Rules**  
To specify the domain names of the queries that you want to forward to DNS resolvers on your network, you create one or more rules\. Each rule specifies one domain name\. You then associate rules with the VPCs for which you want to forward queries to your network\. 

For more information, see the following topics:
+ [Private hosted zones that have overlapping namespaces](hosted-zone-private-considerations.md#hosted-zone-private-considerations-private-overlapping)
+ [Private hosted zones and Route 53 Resolver rules](hosted-zone-private-considerations.md#hosted-zone-private-considerations-resolver-rules)

## Configuring outbound forwarding<a name="resolver-forwarding-outbound-queries-configuring"></a>

To configure Resolver to forward DNS queries that originate in your VPC to your network, perform the following procedures\.

**Important**  
After you create an outbound endpoint, you must create one or more rules and associate them with one or more VPCs\. Rules specify the domain names of the DNS queries that you want to forward to your network\.<a name="resolver-forwarding-outbound-queries-configuring-create-endpoint-procedure"></a>

**To create an outbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Outbound endpoints**\.

1. On the navigation bar, choose the Region where you want to create an outbound endpoint\.

1. Choose **Create outbound endpoint**\.

1. Enter the applicable values\. For more information, see [Values that you specify when you create or edit outbound endpoints](#resolver-forwarding-outbound-queries-endpoint-values)\.

1. Choose **Create**\.
**Note**  
Creating an outbound endpoint takes a minute or two\. You can't create another outbound endpoint until the first one is created\.

1. Create one or more rules to specify the domain names of the DNS queries that you want to forward to your network\. For more information, see the next procedure\.

To create one or more forwarding rules, perform the following procedure\.<a name="resolver-forwarding-outbound-queries-configuring-create-rule-procedure"></a>

**To create forwarding rules and associate the rules with one or more VPCs**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rules**\.

1. On the navigation bar, choose the Region where you want to create the rule\.

1. Choose **Create rule**\.

1. Enter the applicable values\. For more information, see [Values that you specify when you create or edit rules](#resolver-forwarding-outbound-queries-rule-values)\.

1. Choose **Save**\.

1. To add another rule, repeat steps 4 through 6\. 

## Values that you specify when you create or edit outbound endpoints<a name="resolver-forwarding-outbound-queries-endpoint-values"></a>

When you create or edit an outbound endpoint, you specify the following values:

**Endpoint name**  
A friendly name that lets you easily find an outbound endpoint on the dashboard\.

**VPC in the *region\-name* Region**  
All outbound DNS queries will flow through this VPC on the way to your network\.

**Security group for this endpoint**  
The ID of one or more security groups that you want to use to control access to this VPC\. The security group that you specify must include one or more outbound rules\. Outbound rules must allow TCP and UDP access on the port that you're using for DNS queries on your network\.  
For more information, see [Security groups for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the *Amazon VPC User Guide*\.

**IP addresses**  
The IP addresses in your VPC that you want Resolver to forward DNS queries to on the way to resolvers on your network\. These are not the IP addresses of the DNS resolvers on your network; you specify resolver IP addresses when you create the rules that you associate with one or more VPCs\. We require you to specify a minimum of two IP addresses for redundancy\.   
Note the following:    
**Multiple Availability Zones**  
We recommend that you specify IP addresses in at least two Availability Zones\. You can optionally specify additional IP addresses in those or other Availability Zones\.  
**IP addresses and Amazon VPC elastic network interfaces**  
For each combination of Availability Zone, Subnet, and IP address that you specify, Resolver creates an Amazon VPC elastic network interface\. For the current maximum number of DNS queries per second per IP address in an endpoint, see [Quotas on Route 53 Resolver](DNSLimitations.md#limits-api-entities-resolver)\. For information about pricing for each elastic network interface, see "Route 53 Resolver" on the [Amazon Route 53 pricing page](https://aws.amazon.com/route53/pricing/)\.  
**Order of IP addresses**  
You can specify IP addresses in any order\. When forwarding DNS queries, Resolver doesn't choose IP addresses based on the order that the IP addresses are listed in\.
For each IP address, specify the following values\. Each IP address must be in an Availability Zone in the VPC that you specified in **VPC in the *region\-name* Region**\.    
**Availability Zone**  
The Availability Zone that you want DNS queries to pass through on the way to your network\. The Availability Zone that you specify must be configured with a subnet\.  
**Subnet**  
The subnet that contains the IP address that you want DNS queries to originate from on the way to your network\. The subnet must have an available IP address\.  
Specify the subnet for an IPv4 address\. IPv6 is not supported\.  
**IP address**  
The IP address that you want DNS queries to originate from on the way to your network\.  
Choose whether you want Resolver to choose an IP address for you from among the available IP addresses in the specified subnet, or you want to specify the IP address yourself\.  
If you choose to specify the IP address yourself, enter an IPv4 address\. IPv6 is not supported\.

**Tags**  
Specify one or more keys and the corresponding values\. For example, you might specify **Cost center** for **Key** and specify **456** for **Value**\.  
These are the tags that AWS Billing and Cost Management provides for organizing your AWS bill\. For more information about using tags for cost allocation, see [Using cost allocation tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.

## Values that you specify when you create or edit rules<a name="resolver-forwarding-outbound-queries-rule-values"></a>

When you create or edit a forwarding rule, you specify the following values:

**Rule name**  
A friendly name that lets you easily find a rule on the dashboard\.

**Rule type**  
Choose the applicable value:  
+ **Forward** – Choose this option when you want to forward DNS queries for a specified domain name to resolvers on your network\.
+ **System** – Choose this option when you want Resolver to selectively override the behavior that is defined in a forwarding rule\. When you create a system rule, Resolver resolves DNS queries for specified subdomains that would otherwise be resolved by DNS resolvers on your network\.
By default, forwarding rules apply to a domain name and all its subdomains\. If you want to forward queries for a domain to a resolver on your network but you don't want to forward queries for some subdomains, you create a system rule for the subdomains\. For example, if you create a forwarding rule for example\.com but you don't want to forward queries for acme\.example\.com, you create a system rule and specify acme\.example\.com for the domain name\.

**VPCs that use this rule**  
The VPCs that use this rule to forward DNS queries for the specified domain name or names\. You can apply a rule to as many VPCs as you want\.

**Domain name**  
DNS queries for this domain name are forwarded to the IP addresses that you specify in **Target IP addresses**\. For more information, see [How Resolver determines whether the domain name in a query matches any rules](resolver.md#resolver-overview-forward-vpc-to-network-domain-name-matches)\.

**Outbound endpoint**  
Resolver forwards DNS queries through the outbound endpoint that you specify here to the IP addresses that you specify in **Target IP addresses**\.

**Target IP addresses**  
When a DNS query matches the name that you specify in **Domain name**, the outbound endpoint forwards the query to the IP addresses that you specify here\. These are typically the IP addresses for DNS resolvers on your network\.  
**Target IP addresses** is available only when the value of **Rule type** is **Forward**\.  
Specify IPv4 addresses\. IPv6 is not supported\.

**Tags**  
Specify one or more keys and the corresponding values\. For example, you might specify **Cost center** for **Key** and specify **456** for **Value**\.  
These are the tags that AWS Billing and Cost Management provides for organizing your AWS bill\. For more information about using tags for cost allocation, see [Using cost allocation tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.