# Sharing Route 53 Resolver DNS Firewall rule groups between AWS accounts<a name="resolver-dns-firewall-rule-group-sharing"></a>

You can share DNS Firewall rule groups between AWS accounts\. To share rule groups, you use AWS Resource Access Manager \(AWS RAM\)\. The DNS Firewall console integrates with the AWS RAM console\. For more information about AWS RAM, see the [Resource Access Manager User Guide](https://docs.aws.amazon.com/ram/latest/userguide/what-is.html)\.

Note the following:

**Associating shared rule groups with VPCs**  
If another AWS account has shared a rule group with your account, you can associate it with your VPCs the same way that you associate rule groups that you've created\. For more information, see [Managing associations between your VPC and Route 53 Resolver DNS Firewall rule group](resolver-dns-firewall-vpc-associating-rule-group.md)\.

**Deleting or unsharing a shared rule group**  
If you share a rule group with other accounts and then either delete the rule group or stop sharing it, DNS Firewall removes all associations that the other accounts created between the rule group and their VPCs\. 

**Maximum settings for rule groups and associations**  
Shared rule groups and their associations with VPCs are included in the counts for the accounts with which the rule groups are shared\.   
For current DNS Firewall quotas, see [Quotas on Route 53 Resolver DNS Firewall](DNSLimitations.md#limits-api-entities-resolver-dns-firewall)\.

**Permissions**  
To share a rule group with another AWS account, you must have permission to use the [PutFirewallRuleGroupPolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_PutFirewallRuleGroupPolicy.html) action\.

**Restrictions on the AWS account that a rule group is shared with**  
The account that a rule group is shared with can't change or delete the rule group\. 

**Tagging**  
Only the account that created a rule group can add, delete, or see tags on the rule group\.

To view the current sharing status of a rule group \(including the account that shared the rule group or the account that a rule group is shared with\), and to share rule groups with another account, perform the following procedure\.

**To view sharing status and share rule groups with another AWS account**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rule groups**\.

1. On the navigation bar, choose the Region where you created the rule group\.

   The **Sharing status** column shows the current sharing status of rule groups that were created by the current account or that are shared with the current account:
   + **Not shared**: The current AWS account created the rule group, and the rule group is not shared with any other accounts\.
   + **Shared by me**: The current account created the rule group and shared it with one or more accounts\.
   + **Shared with me**: Another account created the rule group and shared it with the current account\.

1. Choose the name of the rule group that you want to display sharing information for or that you want to share with another account\.

   On the **Rule group: *rule group name*** page, the value under **Owner** displays the ID of the account that created the rule group\. That's the current account unless the value of **Sharing status** is **Shared with me**\. In that case, **Owner** is the account that created the rule group and shared it with the current account\.

1. Choose **Share** to view additional information or to share the rule group with another account\. A page in the AWS RAM console appears, depending on the value of **Sharing status**:
   + **Not shared**: The **Create resource share** page appears\. For information about how to share the rule group with another account, organizational unit \(OU\), or organization, go to the step that follows this one\.
   + **Shared by me**: The **Shared resources** page shows the rule groups and other resources that are owned by the current account and shared with other accounts\.
   + **Shared with me**: The **Shared resources** page shows the rule groups and other resources that are owned by other accounts and shared with the current account\.

1. To share a rule group with another AWS account, OU, or organization, specify the following values\.
**Note**  
You can't update sharing settings\. To change any of the following settings, you must reshare a rule group with the new settings and then remove the old sharing settings\.  
**Description**  
Enter a short description that helps you remember why you shared the rule group\.  
**Resources**  
Choose the check box for the rule group that you want to share\.  
**Principals**  
Enter the AWS account number, OU name, or organization name\.  
**Tags**  
Specify one or more keys and the corresponding values\. For example, you might specify **Cost center** for **Key** and specify **456** for **Value**\.  
These are the tags that AWS Billing and Cost Management provides for organizing your AWS bill; you can use also tags for other purposes\. For more information about using tags for cost allocation, see [Using cost allocation tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.