# Managing your own domain lists<a name="resolver-dns-firewall-user-managed-domain-lists"></a>

You can create your own domain lists to specify domain categories that you either don't find in the managed domain list offerings or that you prefer to handle on your own\. 

In addition to the procedures described in this section, in the console, you can create a domain list in the context of Route 53 Resolver DNS Firewall rule management, when you create or update a rule\. 

Each domain specification in your domain list must satisfy the following requirements: 
+ It can optionally start with `*` \(asterisk\)\.
+ With the exception of the optional starting asterisk, it must only contain the following characters: `A-Z`, `a-z`, `0-9`, `-` \(hyphen\)\.
+ It must be from 1\-255 characters in length\. 

When you make changes to DNS Firewall entities, like rules and domain lists, DNS Firewall propagates the changes everywhere that the entities are stored and used\. Your changes are applied within seconds, but there might be a brief period of inconsistency when the changes have arrived in some places and not in others\. So, for example, if you add a domain to a domain list that's referenced by a blocking rule, the new domain might briefly be blocked in one area of your VPC while still allowed in another\. This temporary inconsistency can occur when you first configure your rule group and VPC associations and when you change existing settings\. Generally, any inconsistencies of this type last only a few seconds\.

**Test your domain list before using it in production**  
As a best practice, before using a domain list in production, test it in a non\-production environment, with the rule action set to `Alert`\. Evaluate the rule using Amazon CloudWatch metrics and the Resolver logs\. The logs provide the domain list name for all alerts and blocking actions\. When you're satisfied that the domain list is matching your DNS queries the way you want it to, change the rule action setting as needed\. For information about CloudWatch metrics and the query logs, see [Monitoring Route 53 Resolver DNS Firewall rule groups with Amazon CloudWatch](monitoring-resolver-dns-firewall-with-cloudwatch.md), [Values that appear in Resolver query logs](resolver-query-logs-format.md), and [Managing Resolver query logging configurations](resolver-query-logging-configurations-managing.md)\. 

**To add a domain list**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   \- OR \- 

   Sign in to the AWS Management Console and open the 

   the Amazon VPC console under [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. 

1. Choose **Domain lists**\. In the **Domain lists** page, you can select and edit existing domain lists and you can add your own\.

1. To add a domain list, choose **Add domain list**\. 

1. Provide a name for your domain list, and then enter your domain specifications in the text box, one per line\. 

   If you slide **Switch to bulk upload** to **on**, enter the URI of the Amazon Simple Storage Service bucket where you created a domain list\. This domain list should have one domain name per line\.

1. Choose **Add domain list**\. The **Domain lists** page lists your new domain list\. 

After you create the domain list, you can reference it by name from your DNS Firewall rules\. 

**Deleting DNS Firewall entities**  
When you delete an entity that you can use in DNS Firewall, like a domain list that might be in use in a rule group, or a rule group that might be associated with a VPC, DNS Firewall checks to see if the entity is currently being used\. If it finds that it is in use, DNS Firewall warns you\. DNS Firewall is almost always able to determine if an entity is in use\. However, in rare cases it might not be able to do so\. If you need to be sure that nothing is currently using the entity, check for it in your DNS Firewall configurations before deleting it\. If the entity is a referenced domain list, check that no rule groups are using it\. If the entity is a rule group, check that it is not associated with any VPCs\.

**To delete a domain list**

1. In the navigation pane, choose **Domain lists**\.

1. On the navigation bar, choose the Region for the domain list\. 

1. Select the domain list that you want to delete, then choose **Delete**, and confirm the deletion\.