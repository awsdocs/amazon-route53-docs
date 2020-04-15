# Considerations when working with a private hosted zone<a name="hosted-zone-private-considerations"></a>

When using private hosted zones, note the following considerations\.
+ [Amazon VPC settings](#hosted-zone-private-considerations-vpc-settings)
+ [Route 53 health checks](#hosted-zone-private-considerations-health-checks)
+ [Supported routing policies for records in a private hosted zone](#hosted-zone-private-considerations-routing-policies)
+ [Split-view DNS](#hosted-zone-private-considerations-split-view-dns)
+ [Public and private hosted zones that have overlapping namespaces](#hosted-zone-private-considerations-public-private-overlapping)
+ [Private hosted zones that have overlapping namespaces](#hosted-zone-private-considerations-private-overlapping)
+ [Private hosted zones and Route 53 Resolver rules](#hosted-zone-private-considerations-resolver-rules)
+ [Delegating responsibility for a subdomain](#hosted-zone-private-considerations-delegating-subdomain)
+ [Custom DNS servers](#hosted-zone-private-considerations-custom-dns)
+ [Required IAM permissions](#hosted-zone-private-considerations-required-permissions)

**Amazon VPC settings**  
To use private hosted zones, you must set the following Amazon VPC settings to `true`:  
+ `enableDnsHostnames`
+ `enableDnsSupport`
For more information, see [Updating DNS support for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-updating) in the *Amazon VPC User Guide*\.

**Route 53 health checks**  
In a private hosted zone, you can associate Route 53 health checks only with failover, multivalue answer, and weighted records\. For information about associating health checks with failover records, see [Configuring failover in a private hosted zone](dns-failover-private-hosted-zones.md)\.

**Supported routing policies for records in a private hosted zone**  
You can use the following routing policies when you create records in a private hosted zone:  
+ [Simple routing](routing-policy.md#routing-policy-simple)
+ [Failover routing](routing-policy.md#routing-policy-failover)
+ [Multivalue answer routing](routing-policy.md#routing-policy-multivalue)
+ [Weighted routing](routing-policy.md#routing-policy-weighted)
Creating records in a private hosted zone using other routing policies is not supported\.

**Split\-view DNS**  
You can use Route 53 to configure split\-view DNS, also known as split\-horizon DNS\. In split\-view DNS, you use the same domain name \(example\.com\) for internal uses \(accounting\.example\.com\) and external uses, such as your public website \(www\.example\.com\)\. You might also want to use the same subdomain name internally and externally, but serve different content or require different authentication for internal and external users\.  
To configure split\-view DNS, you perform the following steps:  

1. Create public and private hosted zones that have the same name\. \(Split\-view DNS still works if you're using another DNS service for the public hosted zone\.\)

1. Associate one or more Amazon VPCs with the private hosted zone\. Route 53 Resolver uses the private hosted zone to route DNS queries in the specified VPCs\.

1. Create records in each hosted zone\. Records in the public hosted zone control how internet traffic is routed, and records in the private hosted zone control how traffic is routed in your Amazon VPCs\.
If you need to perform name resolution of both your VPC and on\-premises workloads, you can use Route 53 Resolver\. For more information, see [Resolving DNS queries between VPCs and your network](resolver.md)\.

**Public and private hosted zones that have overlapping namespaces**  
If you have private and public hosted zones that have overlapping namespaces, such as example\.com and accounting\.example\.com, Resolver routes traffic based on the most specific match\. When users are logged into an EC2 instance in an Amazon VPC that you have associated with the private hosted zone, here's how Route 53 Resolver handles DNS queries:  

1. Resolver evaluates whether the name of the private hosted zone matches the domain name in the request, such as accounting\.example\.com\. A match is defined as either of the following:
   + An identical match
   + The name of the private hosted zone is a parent of the domain name in the request\. For example, suppose the domain name in the request is the following:

     **seattle\.accounting\.example\.com**

     The following hosted zones match because they're parents of seattle\.accounting\.example\.com:
     + **accounting\.example\.com**
     + **example\.com**

   If there's no matching private hosted zone, then Resolver forwards the request to a public DNS resolver, and your request is resolved as a regular DNS query\.

1. If there's a private hosted zone name that matches the domain name in the request, the hosted zone is searched for a record that matches the domain name and DNS type in the request, such as an A record for accounting\.example\.com\.
**Note**  
If there's a matching private hosted zone but there's no record that matches the domain name and type in the request, Resolver doesn't forward the request to a public DNS resolver\. Instead, it returns NXDOMAIN \(non\-existent domain\) to the client\.

**Private hosted zones that have overlapping namespaces**  
If you have two or more private hosted zones that have overlapping namespaces, such as example\.com and accounting\.example\.com, Resolver routes traffic based on the most specific match\.   
If you have a private hosted zone \(example\.com\) and a Route 53 Resolver rule that routes traffic to your network for the same domain name, the Resolver rule takes precedence\. See [Private hosted zones and Route 53 Resolver rules](#hosted-zone-private-considerations-resolver-rules)\.
When users are logged into an EC2 instance in an Amazon VPC that you have associated with all of the private hosted zones, here's how Resolver handles DNS queries:  

1. Resolver evaluates whether the domain name in the request, such as accounting\.example\.com, matches the name of one of the private hosted zones\.

1. If there is no hosted zone that exactly matches the domain name in the request, Resolver checks for a hosted zone that has a name that is the parent of the domain name in the request\. For example, suppose the domain name in the request is the following:

   `seattle.accounting.example.com`

   The following hosted zones match because they're parents of `seattle.accounting.example.com`:
   + `accounting.example.com`
   + `example.com`

   Resolver chooses `accounting.example.com` because it's more specific than `example.com`\.

1. Resolver searches the `accounting.example.com` hosted zone for a record that matches the domain name and DNS type in the request, such as an A record for `seattle.accounting.example.com`\.

   If there's no record that matches the domain name and type in the request, Resolver returns NXDOMAIN \(non\-existent domain\) to the client\.

**Private hosted zones and Route 53 Resolver rules**  
If you have a private hosted zone \(example\.com\) and a Resolver rule that routes traffic to your network for the same domain name, the Resolver rule takes precedence\.   
For example, suppose you have the following configuration:  
+ You have a private hosted zone called example\.com, and you associate it with a VPC\.
+ You create a Route 53 Resolver rule that forwards traffic for example\.com to your network, and you associate the rule with the same VPC\.
In this configuration, the Resolver rule takes precedence over the private hosted zone\. DNS queries are forwarded to your network instead of being resolved based on the records in the private hosted zone\.

**Delegating responsibility for a subdomain**  
You cannot create NS records in a private hosted zone to delegate responsibility for a subdomain\.

**Custom DNS servers**  
If you have configured custom DNS servers on Amazon EC2 instances in your VPC, you must configure those DNS servers to route your private DNS queries to the IP address of the Amazon\-provided DNS servers for your VPC\. This IP address is the IP address at the base of the VPC network range "plus two\." For example, if the CIDR range for your VPC is 10\.0\.0\.0/16, the IP address of the DNS server is 10\.0\.0\.2\.  
If you want to route DNS queries between VPCs and your network, you can use Resolver\. For more information, see [Resolving DNS queries between VPCs and your network](resolver.md)\.

**Required IAM permissions**  
To create private hosted zones, you need to grant IAM permissions for Amazon EC2 actions in addition to permissions for Route 53 actions\. For more information, see [Required permissions for actions on private hosted zones](r53-api-permissions-ref.md#required-permissions-private-hosted-zones)\.