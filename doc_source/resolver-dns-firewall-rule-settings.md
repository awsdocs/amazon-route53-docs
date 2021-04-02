# Rule settings in DNS Firewall<a name="resolver-dns-firewall-rule-settings"></a>

When you create or edit a rule in a DNS Firewall rule group, you specify the following values:

**Name**  
A unique identifier for the rule in the rule group\.

**\(Optional\) Description**  
A short description that provides more information about the rule\. 

**Domain list**  
The list of domains that the rule inspects for\. You can create and manage your own domain list or you can subscribe to a domain list that AWS manages for you\. For more information, see [Route 53 Resolver DNS Firewall domain lists](resolver-dns-firewall-domain-lists.md)\. 

**Action**  
How you want DNS Firewall to handle a DNS query whose domain name matches the specifications in the rule's domain list\. For more information, see [Rule actions in DNS Firewall](resolver-dns-firewall-rule-actions.md)\. 

**Priority**  
Unique positive integer setting for the rule within the rule group that determines processing order\. DNS Firewall inspects DNS queries against the rules in a rule group starting with the lowest numeric priority setting and going up\. You can change a rule's priority at any time, for example to change the order of processing or make space for other rules\. 