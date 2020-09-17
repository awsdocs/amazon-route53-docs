# Forwarding inbound DNS queries to your VPCs<a name="resolver-forwarding-inbound-queries"></a>

To forward DNS queries from your network to Resolver, you create an inbound endpoint\. An inbound endpoint specifies the IP addresses \(from the range of IP addresses available to your VPC\) that you want DNS resolvers on your network to forward DNS queries to\. Those IP addresses aren't public IP addresses, so for each inbound endpoint, you need to connect your VPC to your network using either an AWS Direct Connect connection or a VPN connection\.

**Topics**
+ [Configuring inbound forwarding](#resolver-forwarding-inbound-queries-configuring)
+ [Values that you specify when you create or edit inbound endpoints](#resolver-forwarding-inbound-queries-values)

## Configuring inbound forwarding<a name="resolver-forwarding-inbound-queries-configuring"></a>

To create an inbound endpoint, perform the following procedure\.<a name="resolver-forwarding-inbound-queries-configuring-procedure"></a>

**To create an inbound endpoint**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Inbound endpoints**\.

1. On the navigation bar, choose the Region where you want to create an inbound endpoint\.

1. Choose **Create inbound endpoint**\.

1. Enter the applicable values\. For more information, see [Values that you specify when you create or edit inbound endpoints](#resolver-forwarding-inbound-queries-values)\.

1. Choose **Create**\.

1. Configure DNS resolvers on your network to forward the applicable DNS queries to the IP addresses for your inbound endpoint\. For more information, refer to the documentation for your DNS application\.

## Values that you specify when you create or edit inbound endpoints<a name="resolver-forwarding-inbound-queries-values"></a>

When you create or edit an inbound endpoint, you specify the following values:

**Endpoint name**  
A friendly name that lets you easily find an inbound endpoint on the dashboard\.

**VPC in the *region\-name* Region**  
All inbound DNS queries from your network pass through this VPC on the way to Resolver\.

**Security group for this endpoint**  
The ID of one or more security groups that you want to use to control access to this VPC\. The security group that you specify must include one or more inbound rules\. Inbound rules must allow TCP and UDP access on port 53\.  
For more information, see [Security groups for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the *Amazon VPC User Guide*\.

**IP addresses**  
The IP addresses that you want DNS resolvers on your network to forward DNS queries to\. We require you to specify a minimum of two IP addresses for redundancy\. Note the following:    
**Multiple Availability Zones**  
We recommend that you specify IP addresses in at least two Availability Zones\. You can optionally specify additional IP addresses in those or other Availability Zones\.  
**IP addresses and Amazon VPC elastic network interfaces**  
For each combination of Availability Zone, Subnet, and IP address that you specify, Resolver creates an Amazon VPC elastic network interface\. For the current maximum number of DNS queries per second per IP address in an endpoint, see [Quotas on Route 53 Resolver](DNSLimitations.md#limits-api-entities-resolver)\. For information about pricing for each elastic network interface, see "Route 53 Resolver" on the [Amazon Route 53 pricing page](https://aws.amazon.com/route53/pricing/)\.
For each IP address, specify the following values\. Each IP address must be in an Availability Zone in the VPC that you specified in **VPC in the *region\-name* Region**\.    
**Availability Zone**  
The Availability Zone that you want DNS queries to pass through on the way to your VPC\. The Availability Zone that you specify must be configured with a subnet\.  
**Subnet**  
The subnet that contains the IP address that you want to forward DNS queries to\. The subnet must have an available IP address\.  
Specify the subnet for an IPv4 address\. IPv6 is not supported\.  
**IP address**  
The IP address that you want to forward DNS queries to\.  
Choose whether you want Resolver to choose an IP address for you from among the available IP addresses in the specified subnet, or you want to specify the IP address yourself\.  
If you choose to specify the IP address yourself, enter an IPv4 address\. IPv6 is not supported\.

**Tags**  
Specify one or more keys and the corresponding values\. For example, you might specify **Cost center** for **Key** and specify **456** for **Value**\.  
These are the tags that AWS Billing and Cost Management provides for organizing your AWS bill; you can use also tags for other purposes\. For more information about using tags for cost allocation, see [Using cost allocation tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.