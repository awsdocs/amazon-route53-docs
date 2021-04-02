# Enabling Route 53 Resolver DNS Firewall protections for your VPC<a name="resolver-dns-firewall-vpc-protections"></a>

You enable DNS Firewall protections for your VPC by associating one or more rule groups with the VPC\. Whenever a VPC is associated with a DNS Firewall rule group, Route 53 Resolver provides the following DNS Firewall protections: 
+ Resolver routes the VPC's outbound DNS queries through DNS Firewall, and DNS Firewall filters the queries using the associated rule groups\. 
+ Resolver enforces the settings in the VPC's DNS Firewall configuration\. 

To provide DNS Firewall protections to your VPC, you do the following: 
+ Create and manage associations between your DNS Firewall rule groups and your VPC\. For information about rule groups, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\.
+ Configure how you want Resolver to handle DNS queries for the VPC during a failure, for example if DNS Firewall doesn't provide a response for a DNS query\.

**To remove an association between a rule group and a VPC**

1. Locate the rule group's VPC associations by following the instructions in [ the preceding procedure](resolver-dns-firewall-rule-group-sharing.md) **To view a rule group's VPC associations**\. 

1. Select the VPC that you want to remove from the list, then choose **Disassociate**\. Verify, and then confirm the action\. 

On the rule group page, your VPC is listed in the **Associated VPCs** tab with the status of **Disassociating**\. When the operation completes, DNS Firewall updates the list to remove the VPC\. 