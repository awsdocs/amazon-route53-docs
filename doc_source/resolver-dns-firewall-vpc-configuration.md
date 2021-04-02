# DNS Firewall VPC configuration<a name="resolver-dns-firewall-vpc-configuration"></a>

The DNS Firewall configuration for your VPC determines whether Route 53 Resolver allows queries through or blocks them during failures, for example when DNS Firewall is impaired or unresponsive\. Resolver enforces a VPC's firewall configuration whenever you have one or more DNS Firewall rule groups associated with the VPC\.

You can configure a VPC to fail open or fail closed\. 
+ By default, the failure mode is closed, which means that Resolver blocks any queries for which it doesn't receive a reply from DNS Firewall\. This approach favors security over availability\. 
+ If you enable fail open, Resolver allows queries through if it doesn't receive a reply from DNS Firewall\. This approach favors availability over security\. 

**To change the DNS Firewall configuration for a VPC \(console\)**

1. Sign in to the AWS Management Console and open the Resolver console at [https://console\.aws\.amazon\.com/route53resolver/](https://console.aws.amazon.com/route53resolver/)\.

1. In the navigation pane under **Resolvers**, choose **VPCs**\. 

1. In the **VPCs** page, locate and edit the VPC\. Change the DNS Firewall configuration to fail open or fail closed as needed\. 

**To change the DNS Firewall behavior for a VPC \(API\)**
+ Update your VPC firewall configuration by calling [UpdateFirewallConfig](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_UpdateFirewallConfig.html) and enabling or disabling `FirewallFailOpen`\. 

You can retrieve a list of your VPC firewall configurations through the API by calling [ListFirewallConfigs](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListFirewallConfigs.html)\. 