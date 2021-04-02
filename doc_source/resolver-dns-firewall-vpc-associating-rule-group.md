# Managing associations between your VPC and Route 53 Resolver DNS Firewall rule group<a name="resolver-dns-firewall-vpc-associating-rule-group"></a>

**To view a rule group's VPC associations**

1. Sign in to the AWS Management Console and open the Amazon VPC console under [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. 

1. In the navigation pane, locate the **DNS Firewall** section\.

1. In the navigation pane, choose **Rule groups**\.

1. On the navigation bar, choose the Region for the rule group\. 

1. Select the rule group that you want to associate\.

1. Choose **View details**\. The rule group page displays\. 

1. Toward the bottom, you can see a tabbed details area that includes rules and associated VPCs\. Choose the tab **Associated VPCs**\.

**To associate a rule group with a VPC**

1. Locate the rule group's VPC associations by following the instructions in [ the preceding procedure](resolver-dns-firewall-rule-group-sharing.md) **To view a rule group's VPC associations**\. 

1. In the **Associated VPCs** tab, choose **Associate VPC**\.

1. Locate the VPC that you want to associate with the rule group in the dropdown\. Select it, then choose **Associate**\.

In the rule group page, your VPC is listed in the **Associated VPCs** tab\. At first, the association's **Status** reports **Updating**\. When the association is complete, the status changes to **Complete**\. 