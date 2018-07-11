# Considerations When Working with a Private Hosted Zone<a name="hosted-zone-private-considerations"></a>

Note the following considerations when using private hosted zones:

**Amazon VPC Settings**  
To use private hosted zones, you must set the following Amazon VPC settings to `true`:  

+ `enableDnsHostnames`

+ `enableDnsSupport`
For more information, see [Updating DNS Support for Your VPC](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html#vpc-dns-updating) in the *Amazon VPC User Guide*\.

**Route 53 Health Checks**  
In a private hosted zone, you can associate Route 53 health checks only with weighted and failover records\. For information about associating health checks with failover records, see [Configuring Failover in a Private Hosted Zone](dns-failover-private-hosted-zones.md)\.

**Supported Routing Policies for Records in a Private Hosted Zone**  
You can use the following routing policies when you create records in a private hosted zone:  

+ Simple

+ Failover

+ Weighted
Creating records in a private hosted zone using other routing policies is not supported\.

**Split\-View DNS**  
You can use Route 53 to configure split\-view DNS, also known as split\-horizon DNS\. If you want to maintain internal and external versions of the same website or application \(for example, for testing changes before you make them public\), you can configure public and private hosted zones to return different internal and external IP addresses for the same domain name\. Just create a public hosted zone and a private hosted zone that have the same domain name, and create the same subdomains in both hosted zones\.   
If you need to perform name resolution of both your VPC and on\-premises workloads, additional configuration is required\. For more information, see [Hybrid Cloud DNS Solutions for Amazon VPC](https://d1.awsstatic.com/whitepapers/hybrid-cloud-dns-options-for-vpc.pdf)\.

**Associating an Amazon VPC with More than One Private Hosted Zone**  
You can associate a VPC with more than one private hosted zone, but the namespaces must not overlap\. For example, you cannot associate a VPC with hosted zones for both example\.com and acme\.example\.com because both namespaces end with example\.com\. There is no limit on the number of private hosted zones that you can associate a VPC with\.

**Public and Private Hosted Zones That Have Overlapping Namespaces**  
When you have private and public hosted zones that have overlapping namespaces, such as example\.com and accounting\.example\.com, and users are logged into an EC2 instance in an Amazon VPC that you have associated with the private hosted zone, here's how Amazon EC2 handles DNS queries:  

1. Amazon EC2 evaluates whether the name of the private hosted zone matches the domain name in the request, such as accounting\.example\.com\. A match is defined as either of the following:

   + An identical match

   + The name of the private hosted zone is a parent of the domain name in the request\. For example, suppose the domain name in the request is the following:

     **seattle\.accounting\.example\.com**

     The following hosted zones match because they're parents of seattle\.accounting\.example\.com:

     + **accounting\.example\.com**

     + **example\.com**

   If there's no matching private hosted zone, then Amazon EC2 forwards the request to a public DNS resolver, and your request is resolved as a regular DNS query\.

1. If there's a private hosted zone name that matches the domain name in the request, the hosted zone is searched for a record that matches the domain name and DNS type in the request, such as an A record for accounting\.example\.com\.
**Note**  
If there's a matching private hosted zone but there's no record that matches the domain name and type in the request, Amazon EC2 doesn't forward the request to a public DNS resolver\. Instead, it returns NXDOMAIN \(non\-existent domain\) to the client\.

**Delegating Responsibility for a Subdomain**  
You cannot create NS records in a private hosted zone to delegate responsibility for a subdomain\.

**Custom DNS Servers**  
If you have configured custom DNS servers on Amazon EC2 instances in your VPC, you must configure those DNS servers to route your private DNS queries to the IP address of the Amazon\-provided DNS servers for your VPC\. This IP address is the IP address at the base of the VPC network range "plus two\." For example, if the CIDR range for your VPC is 10\.0\.0\.0/16, the IP address of the DNS server is 10\.0\.0\.2\.  
If you're using custom DNS servers that are outside of your VPC and you want to use private DNS, you must reconfigure to use custom DNS servers on Amazon EC2 instances within your VPC\. For more information, see [Amazon DNS Server](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html#AmazonDNS) in the *Amazon VPC User Guide*\.  
If you have integrated your on\-premises network with one or more Amazon VPC virtual networks and you want your on\-premises network to resolve domain names in private hosted zones, you can create a Simple AD directory\. Simple AD provides IP addresses that you can use to submit DNS queries from your on\-premises network to your private hosted zone\. For more information, see [Getting Started with Simple AD](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/getting_started.html) in the *AWS Directory Service Administration Guide*\.

**Required IAM Permissions**  
To create private hosted zones, you need to grant IAM permissions for Amazon EC2 actions in addition to permissions for Route 53 actions\. For more information, see [Required Permissions for Actions on Private Hosted Zones](r53-api-permissions-ref.md#required-permissions-private-hosted-zones)\.