# Managing rule groups and rules in DNS Firewall<a name="resolver-dns-firewall-rule-group-managing"></a>

To manage rule groups and rules in the console, follow the guidance in this topic\.

When you make changes to DNS Firewall entities, like rules and domain lists, DNS Firewall propagates the changes everywhere that the entities are stored and used\. Your changes are applied within seconds, but there might be a brief period of inconsistency when the changes have arrived in some places and not in others\. So, for example, if you add a domain to a domain list that's referenced by a blocking rule, the new domain might briefly be blocked in one area of your VPC while still allowed in another\. This temporary inconsistency can occur when you first configure your rule group and VPC associations and when you change existing settings\. Generally, any inconsistencies of this type last only a few seconds\.

## Creating a rule group and rules<a name="resolver-dns-firewall-rule-group-adding"></a>

**To create a rule group and its rules**

1. Sign in to the AWS Management Console and open the Amazon VPC console under [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. 

1. In the navigation pane, locate the **DNS Firewall** section\.

1. In the navigation pane, choose **Rule groups**\.

1. On the navigation bar, choose the Region for the rule group\. 

1. Choose **Add rule group**, then follow the wizard guidance to specify your rule group and rule settings\.

   For information about the values for rule groups, see [Rule group settings in DNS Firewall](resolver-dns-firewall-rule-group-settings.md)\.

   For information about the values for rules, see [Rule settings in DNS Firewall](resolver-dns-firewall-rule-settings.md)\.

## Viewing and updating a rule group and rules<a name="resolver-dns-firewall-rule-group-editing"></a>

**To view and update a rule group**

1. Sign in to the AWS Management Console and open the Amazon VPC console under [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. 

1. In the navigation pane, locate the **DNS Firewall** section\.

1. In the navigation pane, choose **Rule groups**\.

1. On the navigation bar, choose the Region for the rule group\. 

1. Select the rule group that you want to view or edit, then choose **View details**\. 

1. In the rule group's page, you can view and edit settings\.

   For information about the values for rule groups, see [Rule group settings in DNS Firewall](resolver-dns-firewall-rule-group-settings.md)\.

   For information about the values for rules, see [Rule settings in DNS Firewall](resolver-dns-firewall-rule-settings.md)\.

## Deleting a rule group<a name="resolver-dns-firewall-rule-group-deleting"></a>

To delete a rule group, perform the following procedure\.

**Important**  
If you delete a rule group that's associated with a VPC, DNS Firewall removes the association and stops the protections that the rule group was providing to the VPC\. 

**Deleting DNS Firewall entities**  
When you delete an entity that you can use in DNS Firewall, like a domain list that might be in use in a rule group, or a rule group that might be associated with a VPC, DNS Firewall checks to see if the entity is currently being used\. If it finds that it is in use, DNS Firewall warns you\. DNS Firewall is almost always able to determine if an entity is in use\. However, in rare cases it might not be able to do so\. If you need to be sure that nothing is currently using the entity, check for it in your DNS Firewall configurations before deleting it\. If the entity is a referenced domain list, check that no rule groups are using it\. If the entity is a rule group, check that it is not associated with any VPCs\.

**To delete a rule group**

1. Sign in to the AWS Management Console and open the Amazon VPC console under [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. 

1. In the navigation pane, locate the **DNS Firewall** section\.

1. In the navigation pane, choose **Rule groups**\.

1. On the navigation bar, choose the Region for the rule group\. 

1. Select the rule group that you want to delete, then choose **Delete**, and confirm the deletion\.