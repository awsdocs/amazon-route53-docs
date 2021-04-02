# Route 53 Resolver DNS Firewall domain lists<a name="resolver-dns-firewall-domain-lists"></a>

A *domain list* is a reusable set of domain specifications that you use in a DNS Firewall rule, inside a rule group\. When you associate a rule group with a VPC, DNS Firewall compares your DNS queries against the domain lists that are used in the rules\. If it finds a match, it handles the DNS query according to the matching rule's action\. For more information about rule groups and rules, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\. 

Domain lists allow you to separate your explicit domain specifications from the actions that you want to take on them\. You can use a single domain list in multiple rules and any updates that you do to the domain list automatically affects all rules that use it\. 

Domain lists fall into two main categories: 
+ Managed domain lists, which AWS creates and maintains for you\.
+ Your own domain lists, which you create and maintain\.

This section describes the types of managed domain lists that are available to you and provides guidance for creating and managing your own domain lists, if you choose to do so\. 