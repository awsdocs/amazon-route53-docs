# Managing forwarding rules<a name="resolver-rules-managing"></a>

If you want Resolver to forward queries for specified domain names to your network, you create one forwarding rule for each domain name and specify the name of the domain for which you want to forward queries\.

**Topics**
+ [Viewing and editing forwarding rules](#resolver-rules-managing-viewing)
+ [Creating forwarding rules](#resolver-rules-managing-creating-rules)
+ [Adding rules for reverse lookup](#add-reverse-lookup)
+ [Associating forwarding rules with a VPC](#resolver-rules-managing-associating-rules)
+ [Disassociating forwarding rules from a VPC](#resolver-rules-managing-disassociating-rules)
+ [Sharing forwarding rules with other AWS accounts and using shared rules](#resolver-rules-managing-sharing)
+ [Deleting forwarding rules](#resolver-rules-managing-deleting)

## Viewing and editing forwarding rules<a name="resolver-rules-managing-viewing"></a>

To view and edit settings for a forwarding rule, perform the following procedure\.<a name="resolver-rules-managing-viewing-procedure"></a>

**To view and edit settings for a forwarding rule**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rules**\.

1. On the navigation bar, choose the Region where you created the rule\.

1. Choose the option for the rule that you want to view settings for or want to edit\.

1. Choose **View details** or **Edit**\.

   For information about the values for forwarding rules, see [Values that you specify when you create or edit rules](resolver-forwarding-outbound-queries.md#resolver-forwarding-outbound-queries-rule-values)\.

1. If you chose **Edit**, enter the applicable values, and then choose **Save**\.

## Creating forwarding rules<a name="resolver-rules-managing-creating-rules"></a>

To create one or more forwarding rules, perform the following procedure\.<a name="resolver-rules-managing-creating-rules-procedure"></a>

**To create forwarding rules and associate the rules with one or more VPCs**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rules**\.

1. On the navigation bar, choose the Region where you want to create the rule\.

1. Choose **Create rule**\.

1. Enter the applicable values\. For more information, see [Values that you specify when you create or edit rules](resolver-forwarding-outbound-queries.md#resolver-forwarding-outbound-queries-rule-values)\.

1. Choose **Save**\.

1. To add another rule, repeat steps 4 through 6\. 

## Adding rules for reverse lookup<a name="add-reverse-lookup"></a>

If you need to control reverse lookups in your VPC, you can add rules to your outbound resolver endpoint\.

**To create the reverse lookup rule**

1. Follow the steps in the previous procedure, up to step 5\.

1. When you specify your rule, enter the PTR record for the IP address or addresses that you want a reverse lookup forwarding rule for\.

   For example, if you need to forward lookups for addresses in the 10\.0\.0\.0/23 range, enter two rules:
   + 0\.0\.10\.in\-addr\.apra
   + 1\.0\.10\.in\-addr\.apra

   Any IP address in those subnets will be referenced as a subdomain of those PTR records—for example, 10\.0\.1\.161 will have a reverse lookup address of 161\.1\.0\.10\.in\-addr\.apra, which is a subdomain of 1\.0\.10\.in\-addra\.apra\.

1. Specify the server to forward these lookups to\.

1. Add these rules to your outbound resolver endpoint\.

Note that turning on `enableDNSHostNames` for your VPC will automatically add PTR records\. See [Resolving DNS queries between VPCs and your network](resolver.md)\. The previous procedure is only required if you want to explicitly specify a resolver for given IP ranges—for example, when forwarding queries to an Active Directory server\.

## Associating forwarding rules with a VPC<a name="resolver-rules-managing-associating-rules"></a>

After you create a forwarding rule, you must associate the rule with one or more VPCs\. When you associate a rule with a VPC, Resolver starts to forward DNS queries for the domain name that's specified in the rule to the DNS resolvers that you specified in the rule\. The queries pass through the outbound endpoint that you specified when you created the rule\.<a name="resolver-rules-managing-associating-procedure"></a>

**To associate a forwarding rule with one or more VPCs**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rules**\.

1. On the navigation bar, choose the Region where you created the rule\.

1. Choose the name of the rule that you want to associate with one or more VPCs\.

1. Choose **Associate VPC**\.

1. Under **VPCs that use this rule**, choose the VPCs that you want to associate the rule with\.

1. Choose **Add**\.

## Disassociating forwarding rules from a VPC<a name="resolver-rules-managing-disassociating-rules"></a>

You disassociate a forwarding rule from a VPC in the following circumstances:
+ For DNS queries that originate in this VPC, you want Resolver to stop forwarding queries for the domain name specified in the rule to your network\. 
+ You want to delete the forwarding rule\. If a rule is currently associated with one or more VPCs, you must disassociate the rule from all VPCs before you can delete it\.

If you want to disassociate a forwarding rule from one or more VPCs, perform the following procedure\.<a name="resolver-rules-managing-disassociating-procedure"></a>

**To disassociate a forwarding rule from a VPC**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rules**\.

1. On the navigation bar, choose the Region where you created the rule\.

1. Choose the name of the rule that you want to disassociate from one or more VPCs\.

1. Choose the option for the VPC that you want to disassociate the rule from\.

1. Choose **Disassociate**\.

1. Type **disassociate** to confirm\.

1. Choose **Submit**\.

## Sharing forwarding rules with other AWS accounts and using shared rules<a name="resolver-rules-managing-sharing"></a>

You can share the forwarding rules that you created using one AWS account with other AWS accounts\. To share rules, the Route 53 Resolver console integrates with AWS Resource Access Manager\. For more information about Resource Access Manager, see the [Resource Access Manager User Guide](https://docs.aws.amazon.com/ram/latest/userguide/what-is.html)\.

Note the following:

**Associating shared rules with VPCs**  
If another AWS account has shared one or more rules with your account, you can associate the rules with your VPCs the same way that you associate rules that you created with your VPCs\. For more information, see [Associating forwarding rules with a VPC](#resolver-rules-managing-associating-rules)\.

**Deleting or unsharing a rule**  
If you share a rule with other accounts and then either delete the rule or stop sharing it, and if the rule was associated with one or more VPCs, Route 53 Resolver starts to process DNS queries for those VPCs based on the remaining rules\. The behavior is the same as if you disassociate the rule from the VPC\.

**Maximum number of rules and associations**  
When an account creates a rule and shares it with one or more other accounts, the maximum number of rules per AWS Region applies to the account that created the rule\.  
When an account that a rule is shared with associates the rule with one or more VPCs, the maximum number of associations between rules and VPCs per Region applies to the account that the rule is shared with\.  
For current Resolver quotas, see [Quotas on Route 53 Resolver](DNSLimitations.md#limits-api-entities-resolver)\.

**Permissions**  
To share a rule with another AWS account, you must have permission to use the [PutResolverRulePolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_PutResolverRulePolicy.html) action\.

**Restrictions on the AWS account that a rule is shared with**  
The account that a rule is shared with can't change or delete the rule\. 

**Tagging**  
Only the account that created a rule can add, delete, or see tags on the rule\.

To view the current sharing status of a rule \(including the account that shared the account or the account that a rule is shared with\), and to share rules with another account, perform the following procedure\.<a name="resolver-rules-managing-sharing-procedure"></a>

**To view sharing status and share rules with another AWS account**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rules**\.

1. On the navigation bar, choose the Region where you created the rule\.

   The **Sharing status** column shows the current sharing status of rules that were created by the current account or that are shared with the current account:
   + **Not shared**: The current AWS account created the rule, and the rule is not shared with any other accounts\.
   + **Shared by me**: The current account created the rule and shared it with one or more accounts\.
   + **Shared with me**: Another account created the rule and shared it with the current account\.

1. Choose the name of the rule that you want to display sharing information for or that you want to share with another account\.

   On the **Rule: *rule name*** page, the value under **Owner** displays ID of the account that created the rule\. That's the current account unless the value of **Sharing status** is **Shared with me**\. In that case, **Owner** is the account that created the rule and shared it with the current account\.

1. Choose **Share** to view additional information or to share the rule with another account\. A page in the Resource Access Manager console appears, depending on the value of **Sharing status**:
   + **Not shared**: The **Create resource share** page appears\. For information about how to share the rule with another account, OU, or organization, skip to step 6\.
   + **Shared by me**: The **Shared resources** page shows the rules and other resources that are owned by the current account and shared with other accounts\.
   + **Shared with me**: The **Shared resources** page shows the rules and other resources that are owned by other accounts and shared with the current account\.

1. To share a rule with another AWS account, OU, or organization, specify the following values\.
**Note**  
You can't update sharing settings\. If you want to change any of the following settings, you must reshare a rule with the new settings and then remove the old sharing settings\.  
**Description**  
Enter a short description that helps you remember why you shared the rule\.  
**Resources**  
Choose the check box for the rule that you want to share\.  
**Principals**  
Enter the AWS account number, OU name, or organization name\.  
**Tags**  
Specify one or more keys and the corresponding values\. For example, you might specify **Cost center** for **Key** and specify **456** for **Value**\.  
These are the tags that AWS Billing and Cost Management provides for organizing your AWS bill; you can use also tags for other purposes\. For more information about using tags for cost allocation, see [Using cost allocation tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.

## Deleting forwarding rules<a name="resolver-rules-managing-deleting"></a>

To delete a forwarding rule, perform the following procedure\.

Note the following:
+ If the forwarding rule is associated with any VPCs, you must disassociate the rule from the VPCs before you can delete the rule\. For more information, see [Disassociating forwarding rules from a VPC](#resolver-rules-managing-disassociating-rules)\.
+ You can't delete the default **Internet Resolver** rule, which has a value of **Recursive** for **Type**\. This rule causes Route 53 Resolver to act as a recursive resolver for any domain names that you didn't create custom rules for and that Resolver didn't create autodefined rules for\. For more information about how rules are categorized, see [Using rules to control which queries are forwarded to your network](resolver.md#resolver-overview-forward-vpc-to-network-using-rules)\.<a name="resolver-rules-managing-deleting-procedure"></a>

**To delete a forwarding rule**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Rules**\.

1. On the navigation bar, choose the Region where you created the rule\.

1. Choose the option for the rule that you want to delete\.

1. Choose **Delete**\.

1. To confirm that you want to delete the rule, enter the name of the rule and choose **Submit**\.