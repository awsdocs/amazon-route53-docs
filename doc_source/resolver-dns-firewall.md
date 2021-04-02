# Route 53 Resolver DNS Firewall<a name="resolver-dns-firewall"></a>

With Route 53 Resolver DNS Firewall, you can filter and regulate outbound DNS traffic for your virtual private connections \(VPCs\)\. To do this, you create reusable collections of filtering rules in DNS Firewall rule groups, associate the rule groups to your VPC, and then monitor activity in DNS Firewall logs and metrics\. Based on the activity, you can adjust the behavior of DNS Firewall accordingly\. 

DNS Firewall provides protection for outbound DNS requests from your VPCs\. These requests route through Resolver for domain name resolution\. A primary use of DNS Firewall protections is to help prevent DNS exfiltration of your data\. DNS exfiltration can happen when a bad actor compromises an application instance in your VPC and then uses DNS lookup to send data out of the VPC to a domain that they control\. With DNS Firewall, you can monitor and control the domains that your applications can query\. You can deny access to the domains that you know to be bad and allow all other queries to pass through\. Alternately, you can deny access to all domains except for the ones that you explicitly trust\. 

DNS Firewall is a feature of Route 53 Resolver and doesn't require any additional Resolver setup to use\. 

**AWS Firewall Manager supports DNS Firewall**  
You can use Firewall Manager to centrally configure and manage your DNS Firewall rule group associations for your VPCs across your accounts in AWS Organizations\. Firewall Manager automatically adds associations for VPCs that come into scope of your Firewall Manager DNS Firewall policy\. For more information, see [AWS Firewall Manager](https://docs.aws.amazon.com/waf/latest/developerguide/fms-chapter.html) in the *AWS WAF, AWS Firewall Manager, and AWS Shield Advanced Developer Guide*\.

**How DNS Firewall works with AWS Network Firewall**  
DNS Firewall and Network Firewall both offer domain name filtering, but for different types of traffic\. With DNS Firewall and Network Firewall together, you can configure domain\-based filtering for application layer traffic over two different network paths\. 
+ DNS Firewall provides filtering for outbound DNS queries that pass through the Route 53 Resolver from applications within your VPCs\. You can also configure DNS Firewall to send custom responses for queries to blocked domain names\. 
+ Network Firewall provides filtering for both network and application layer traffic, but does not have visibility into queries made by Route 53 Resolver\. 

For more information about Network Firewall, see the [Network Firewall Developer Guide](https://docs.aws.amazon.com/network-firewall/latest/developerguide/what-is-aws-network-firewall.html)\.