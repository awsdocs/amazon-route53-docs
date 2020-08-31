# Sharing Resolver query logging configurations with other AWS accounts<a name="query-logging-configurations-managing-sharing"></a>

You can share the query logging configurations that you created using one AWS account with other AWS accounts\. To share configurations, the Route 53 Resolver console integrates with AWS Resource Access Manager\. For more information about Resource Access Manager, see the [Resource Access Manager User Guide](https://docs.aws.amazon.com/ram/latest/userguide/what-is.html)\.

Note the following:

**Associating VPCs with shared query logging configurations**  
If another AWS account has shared one or more configurations with your account, you can associate VPCs with the configuration the same way that you associate VPCs with configurations that you created\.

**Deleting or unsharing a configuration**  
If you share a configuration with other accounts and then either delete the configuration or stop sharing it, and if one or more VPCs were associated with the configuration, Route 53 Resolver stops logging DNS queries that originate in those VPCs\.

**Maximum number of query logging configurations and VPCs that can be associated with a config**  
When an account creates a configuration and shares it with one or more other accounts, the maximum number of VPCs that can be associated with the configuration applies to the account that created the rule\.  
For current Resolver quotas, see [Quotas on Route 53 Resolver](DNSLimitations.md#limits-api-entities-resolver)\.

**Permissions**  
To share a rule with another AWS account, you must have permission to use the [PutResolverQueryLogConfigPolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_PutResolverQueryLogConfigPolicy.html) action\.

**Restrictions on the AWS account that a rule is shared with**  
The account that a rule is shared with can't change or delete the rule\. 

**Tagging**  
Only the account that created a rule can add, delete, or see tags on the rule\.

To view the current sharing status of a rule \(including the account that shared the account or the account that a rule is shared with\), and to share rules with another account, perform the following procedure\.<a name="resolver-rules-managing-sharing-procedure"></a>

**To view sharing status and share query logging configurations with another AWS account**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Query Logging**\.

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

1. To share a query logging configuration with another AWS account, OU, or organization, specify the following values\.
**Note**  
You can't update sharing settings\. If you want to change any of the following settings, you must reshare a rule with the new settings and then remove the old sharing settings\.  
**Description**  
Enter a short description that helps you remember why you shared the query logging configuration\.  
**Resources**  
Choose the check box for the configuration that you want to share\.  
**Principals**  
Enter the AWS account number, OU name, or organization name\.  
**Tags**  
Specify one or more keys and the corresponding values\. For example, you might specify **Cost center** for **Key** and specify **456** for **Value**\.  
These are the tags that AWS Billing and Cost Management provides for organizing your AWS bill; you can use also tags for other purposes\. For more information about using tags for cost allocation, see [Using cost allocation tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the *AWS Billing and Cost Management User Guide*\.