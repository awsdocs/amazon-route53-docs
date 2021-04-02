# How Route 53 Resolver DNS Firewall works<a name="resolver-dns-firewall-overview"></a>

Route 53 Resolver DNS Firewall lets you control access to sites and block DNS\-level threats for DNS queries going out from your VPC through the Route 53 Resolver\. With DNS Firewall, you define domain name filtering rules in rule groups that you associate with your VPCs\. You can specify lists of domain names to allow or block, and you can customize the responses for the DNS queries that you block\. 

DNS Firewall only filters on the domain name\. It does not resolve that name to an IP address to be blocked\. Additionally, DNS Firewall filters DNS/UDP traffic, but it doesn't filter other application layer protocols, such as HTTPS, SSH, TLS, FTP, and so on\.

## Route 53 Resolver DNS Firewall components and settings<a name="resolver-dns-firewall-components"></a>

You manage DNS Firewall with the following central components and settings\.

**DNS Firewall rule group**  
Defines a named, reusable collection of DNS Firewall rules for filtering DNS queries\. You populate the rule group with the filtering rules, then associate the rule group with one or more VPCs\. When you associate a rule group with a VPC, you enable DNS Firewall filtering for the VPC\. Then, when Resolver receives a DNS query for a VPC that has a rule group associated with it, Resolver passes the query to DNS Firewall for filtering\.   
If you associate multiple rule groups with a single VPC, you indicate their processing order through the priority setting in each association\. DNS Firewall processes rule groups for a VPC from the lowest numeric priority setting on up\.   
For more information, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\. 

**DNS Firewall rule**  
Defines a filtering rule for DNS queries in a DNS Firewall rule group\. Each rule specifies one domain list and an action to take on DNS queries whose domains match the domain specifications in the list\. You can allow, block, or alert on matching queries\. You can also define custom responses for blocked queries\.   
Each rule in a rule group has a priority setting that's unique within the rule group\. DNS Firewall processes the rules in a rule group from the lowest numeric priority setting on up\.   
DNS Firewall rules exist only in the context of the rule group in which they're defined\. You can't reuse a rule or reference it independent of its rule group\.   
For more information, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\. 

**Domain list**  
Defines a named, reusable collection of domain specifications for use in DNS filtering\. Each rule in a rule group requires a single domain list\. You might choose to specify the domains that you want to allow access to, the domains that you want to deny access to, or a combination of both\. You can create your own domain lists and you can use domain lists that AWS manages for you\.  
For more information, see [Route 53 Resolver DNS Firewall domain lists](resolver-dns-firewall-domain-lists.md)\. 

**Association between a DNS Firewall rule group and a VPC**  
Defines a protection for a VPC using a DNS Firewall rule group and enables the Resolver DNS Firewall configuration for the VPC\.   
If you associate multiple rule groups with a single VPC, you indicate their processing order through the priority setting in the associations\. DNS Firewall processes rule groups for a VPC from the lowest numeric priority setting on up\.   
For more information, see [Enabling Route 53 Resolver DNS Firewall protections for your VPC](resolver-dns-firewall-vpc-protections.md)\. 

**Resolver DNS Firewall configuration for a VPC**  
Specifies how Resolver should handle DNS Firewall protections at the VPC level\. This configuration is in effect whenever you have at least one DNS Firewall rule group associated with the VPC\.   
This configuration specifies how Route 53 Resolver handles queries when DNS Firewall fails to filter them\. By default, if Resolver doesn't receive a response from DNS Firewall for a query, it fails closed and blocks the query\.  
For more information, see [DNS Firewall VPC configuration](resolver-dns-firewall-vpc-configuration.md)\.

## How Route 53 Resolver DNS Firewall filters DNS queries<a name="resolver-dns-firewall-behavior"></a>

When a DNS Firewall rule group is associated with your VPC, Route 53 Resolver sends the following traffic to it for filtering the following queries:
+ Outbound DNS queries from the VPC\.
+ DNS queries that pass through Resolver endpoints between cloud resources and on\-premises resources, in either direction\.

When DNS Firewall receives a DNS query, it filters the query using the rule groups, rules, and other settings that you've configured and sends the results back to Resolver: 
+ DNS Firewall evaluates the DNS query using the rule groups that are associated with the VPC until it finds a match or exhausts all of the rule groups\. DNS Firewall evaluates the rule groups in order of the priority that you set in the association, starting with the lowest numeric setting\. For more information, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md) and [Enabling Route 53 Resolver DNS Firewall protections for your VPC](resolver-dns-firewall-vpc-protections.md)\.
+ Within each rule group, DNS Firewall evaluates the DNS query against each rule's domain list until it finds a match or exhausts all rules\. DNS Firewall evaluates the rules in order of priority, starting with the lowest numeric setting\. For more information, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\.
+ When DNS Firewall finds a match with a rule's domain list, it terminates the query evaluation and responds to Resolver with the result\. If the action is `alert`, DNS Firewall also sends an alert to the configured Resolver logs\. For more information, see [Rule actions in DNS Firewall](resolver-dns-firewall-rule-actions.md) and [Route 53 Resolver DNS Firewall domain lists](resolver-dns-firewall-domain-lists.md)\.
+ If DNS Firewall evaluates all rule groups without finding a match, it responds to Resolver to the query as normal\. 

Resolver routes the query according to the response from DNS Firewall\. In the unlikely event that DNS Firewall fails to respond, Resolver applies the VPC's configured DNS Firewall fail mode\. For more information, see [DNS Firewall VPC configuration](resolver-dns-firewall-vpc-configuration.md)\.

## High\-level steps for using Route 53 Resolver DNS Firewall<a name="resolver-dns-firewall-high-level-steps"></a>

To implement Route 53 Resolver DNS Firewall filtering in your Amazon Virtual Private Cloud VPC, you perform the following high\-level steps\. 
+ **Define your filtering approach and your domain lists** – Decide how you want to filter queries, identify the domain specifications that you'll need, and define the logic you'll use to evaluate queries\. For example, you might want to allow all queries except for those that are in a list of known bad domains\. Or you might want to do the opposite and block all but an approved list of domains, in what is known as a walled garden approach\. You can create and manage your own lists of approved or blocked domain specifications and you can use domain lists that AWS manages for you\.For information about domain lists, see [Route 53 Resolver DNS Firewall domain lists](resolver-dns-firewall-domain-lists.md)\.
+ **Create a firewall rule group** – In DNS Firewall, create a rule group to filter DNS queries for your VPC\. You must create a rule group in each Region where you want to use it\. You might also want to separate your filtering behavior into more than one rule group for reusability in multiple filtering scenarios for your different VPCs\. For information about rule groups, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\. 
+ **Add and configure your rules** – Add a rule to your rule group for each domain list and filtering behavior that you want the rule group to provide\. Set the priority settings for your rules so they process in the correct order within the rule group, giving the lowest priority to the rule that you want to evaluate first\. For information about rules, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\. 
+ **Associate the rule group to your VPC** – To begin using your DNS Firewall rule group, associate it with your VPC\. If you are using more than one rule group for your VPC, set the priority of each association so the rule groups are processed in the correct order, giving the lowest priority to the rule group that you want to evaluate first\. For more information, see [Managing associations between your VPC and Route 53 Resolver DNS Firewall rule group](resolver-dns-firewall-vpc-associating-rule-group.md)\.
+ **\(Optional\) Change the firewall configuration for the VPC** – If you want Route 53 Resolver to block queries when DNS Firewall fails to send a response back for them, in Resolver, change the VPC's DNS Firewall configuration\. For more information, see [DNS Firewall VPC configuration](resolver-dns-firewall-vpc-configuration.md)\.

## Using Route 53 Resolver DNS Firewall rule groups in multiple Regions<a name="resolver-dns-firewall-multiple-regions"></a>

Route 53 Resolver DNS Firewall is a Regional service, so objects that you create in one AWS Region are available only in that Region\. To use the same rule group in more than one Region, you must create it in each Region\.

The AWS account that created a rule group can share it with other AWS accounts\. For more information, see [Sharing Route 53 Resolver DNS Firewall rule groups between AWS accounts](resolver-dns-firewall-rule-group-sharing.md)\.