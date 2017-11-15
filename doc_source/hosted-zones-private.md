# Working with Private Hosted Zones<a name="hosted-zones-private"></a>

A private hosted zone is a container that holds information about how you want to route traffic for a domain and its subdomains within one or more Amazon Virtual Private Clouds \(Amazon VPCs\)\. To begin, you create a private hosted zone and specify the Amazon VPCs that you want to associate with the hosted zone\. You then create resource record sets that determine how Amazon Route 53 responds to queries for your domain and subdomains within and among your Amazon VPCs\. For example, if you have a web server associated with your domain, you'll create an A record in your hosted zone so browser queries for example\.com are routed to your web server\. For more information about resource record sets, see [Working with Resource Record Sets](rrsets-working-with.md)\. For information about the Amazon VPC requirements for using private hosted zones, see [Using Private Hosted Zones](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html#vpc-private-hosted-zones) in the *Amazon VPC User Guide*\.

Note the following about using private hosted zones:

**Amazon VPC Settings**  
To use private hosted zones, you must set the following Amazon VPC settings to `true`:  

+ `enableDnsHostnames`

+ `enableDnsSupport`
For more information, see [Updating DNS Support for Your VPC](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html#vpc-dns-updating) in the *Amazon VPC User Guide*\.

**Amazon Route 53 Health Checks**  
In a private hosted zone, you can associate Amazon Route 53 health checks only with failover resource record sets\. For more information, see [Configuring Failover in a Private Hosted Zone](dns-failover-private-hosted-zones.md)\.

**Supported Routing Policies for Resource Record Sets in a Private Hosted Zone**  
You can use the following routing policies when you create resource record sets in a private hosted zone:  

+ Simple

+ Failover

+ Weighted
Creating resource record sets in a private hosted zone using geolocation or latency routing policies is not supported\.

**Split\-View DNS**  
You can use Amazon Route 53 to configure split\-view DNS, also known as split\-horizon DNS\. If you want to maintain internal and external versions of the same website or application \(for example, for testing changes before you make them public\), you can configure public and private hosted zones to return different internal and external IP addresses for the same domain name\. Just create a public hosted zone and a private hosted zone that have the same domain name, and create the same subdomains in both hosted zones\. 

**Associating an Amazon VPC with More than One Private Hosted Zone**  
You can associate a VPC with more than one private hosted zone, but the namespaces must not overlap\. For example, you cannot associate a VPC with hosted zones for both example\.com and acme\.example\.com because both namespaces end with example\.com\. 

**Public and Private Hosted Zones that Have Overlapping Name Spaces**  
When you have private and public hosted zones that have overlapping name spaces, such as example\.com and accounting\.example\.com, and users are logged into an EC2 instance in an Amazon VPC that you have associated with the private hosted zone, here's how Amazon EC2 handles DNS queries:  

1. Amazon EC2 evaluates whether the name of the private hosted zone matches the domain name in the request, such as accounting\.example\.com\. A match is defined as either of the following:

   + An identical match

   + The name of the private hosted zone is a parent of the domain name in the request\. For example, suppose the domain name in the request is the following:

     **seattle\.accounting\.example\.com**

     The following hosted zones match because they're parents of seattle\.accounting\.example\.com:

     + **accounting\.example\.com**

     + **example\.com**

   If there's no matching private hosted zone, then Amazon EC2 forwards the request to a public DNS resolver, and your request is resolved as a regular DNS query\.

1. If there's a private hosted zone name that matches the domain name in the request, the hosted zone is searched for a resource record set that matches the domain name and DNS type in the request, such as an A record for accounting\.example\.com\.
**Note**  
If there's a matching private hosted zone but there's no resource record set that matches the domain name and type in the request, Amazon EC2 doesn't forward the request to a public DNS resolver\. Instead, it returns NXDOMAIN to the client\.

**Delegating Responsibility for a Subdomain**  
You cannot create NS records in a private hosted zone to delegate responsibility for a subdomain\.

**Custom DNS Servers**  
If you have configured custom DNS servers on Amazon EC2 instances in your VPC, you must configure those DNS servers to route your private DNS queries to the IP address of the Amazon\-provided DNS servers for your VPC\. This IP address is the IP address at the base of the VPC network range "plus two\." For example, if the CIDR range for your VPC is 10\.0\.0\.0/16, the IP address of the DNS server is 10\.0\.0\.2\.  
If you're using custom DNS servers that are outside of your VPC and you want to use private DNS, you must reconfigure to use custom DNS servers on Amazon EC2 instances within your VPC\. For more information, see [Amazon DNS Server](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html#AmazonDNS) in the *Amazon VPC User Guide*\.  
If you have integrated your on\-premises network with one or more Amazon VPC virtual networks and you want your on\-premises network to resolve domain names in private hosted zones, you can create a Simple AD directory\. Simple AD provides IP addresses that you can use to submit DNS queries from your on\-premises network to your private hosted zone\. For more information, see [Getting Started with Simple AD](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/getting_started.html) in the *AWS Directory Service Administration Guide*\.

**Required IAM Permissions**  
To create private hosted zones, you need to grant IAM permissions for Amazon EC2 actions in addition to permissions for Amazon Route 53 actions\. For more information, see [Required Permissions for Actions on Private Hosted Zones](r53-api-permissions-ref.md#required-permissions-private-hosted-zones)\.

This topic explains how to use the Amazon Route 53 console to create, list, and delete private hosted zones\. For information about using the Amazon Route 53 API to perform these operations, see the [Amazon Route 53 API Reference](http://docs.aws.amazon.com/Route53/latest/APIReference/)\.

You can also use an Amazon Route 53 *public* hosted zone to route traffic for your domain on the internet\. For more information, see [Working with Public Hosted Zones](AboutHZWorkingWith.md)\.


+ [Creating a Private Hosted Zone](hosted-zone-private-creating.md)
+ [Listing Private Hosted Zones](hosted-zone-private-listing.md)
+ [Associating More Amazon VPCs with a Private Hosted Zone](hosted-zone-private-associate-vpcs.md)
+ [Associating an Amazon VPC and a Private Hosted Zone That You Created with Different AWS Accounts](hosted-zone-private-associate-vpcs-different-accounts.md)
+ [Disassociating Amazon VPCs from a Private Hosted Zone](hosted-zone-private-disassociate-vpcs.md)
+ [Deleting a Private Hosted Zone](hosted-zone-private-deleting.md)