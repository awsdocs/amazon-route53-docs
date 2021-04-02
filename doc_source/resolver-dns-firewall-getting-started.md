# Getting started with Route 53 Resolver DNS Firewall<a name="resolver-dns-firewall-getting-started"></a>

The DNS Firewall console includes a wizard that guides you through the following steps for getting started with DNS Firewall:
+ Create rule groups for each set of rules that you want to use\.
+ For each rule, populate the domain list that you want to inspect for\. You can create your own domain lists and you can use AWS managed domain lists\. 
+ Associate your rule groups with the VPCs where you want to use them\.

In this tutorial, you'll create a rule group that blocks all but a select group of domains\. This is called a closed platform, or walled garden approach\.

**To configure a DNS Firewall rule group using the console wizard**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   \- OR \- 

   Sign in to the AWS Management Console and open the 

   the Amazon VPC console under [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. 

1. In the navigation pane, choose **Rule groups**\.

1. On the navigation bar, choose the Region for the rule group\. 

1. In the **Rule groups** page, choose **Add rule group**\.

1. For the rule group name, enter **WalledGardenExample**\. If you want an additional description, enter that as well\.

1. Choose **Next**\.

1. On the **Add rules** page, choose **Add rule**\.

   1. In the **Rule details** pane, enter the rule name **BlockAll**\.

   1. In the **Domain list** pane, select **Add my own domain list**\. 

   1. Under **Choose or create a new domain list** select **Create new domain list**\.

   1. Enter a domain list name **AllDomains**, then in the text box, enter an asterisk: **\***\. 

   1. For the action, select **BLOCK** and then leave the response to send at the default setting of **NODATA**\. 

   1. Choose **Add rule**\. The wizard displays the rule group's **Add rules** page with your **BlockAll** rule listed\.

1. Choose **Add rule** again to add a second rule to your rule group\. 

   1. In the **Rule details** pane, enter the rule name **AllowSelectDomains** and leave the description empty\.

   1. In the **Domain list** pane, select **Add my own domain list**\. 

   1. Under **Choose or create a new domain list**, select **Create new domain list**\.

   1. Enter a domain list name **ExampleDomains**\.

   1. In the text box, on the first line, enter **example\.com** and on the second line, enter **example\.org**\. 

   1. For the action, select **ALLOW**\. 

   1. Choose **Add rule**\. The wizard displays the **Add rules** page with your two rules listed\.

1. Choose **Next**\.

1. In the **Set rule priority** page, you can adjust the evaluation order of the rules in your rule group\. DNS Firewall evaluates rules starting with the lowest priority setting, so the rule at the top of the list is the first one evaluated\. For this example, we want DNS Firewall to first identify and allow DNS queries for the select list of domains, and then block any remaining queries\. 

   Select and adjust the rule ordering so that **AllowSelectDomains** is listed first\.

1. Choose **Next**\.

1. In the **Add tags** page, choose **Next**\. Tags help you organize and manage your AWS resources\. For more information, see [Tagging Amazon Route 53 resources](tagging-resources.md)\. 

1. On the **Review and create** page, confirm that the settings that you specified on the previous pages are correct\. If necessary, choose **Edit** for the applicable section, and update settings\. When you're satisfied with the settings, choose **Create rule group**\. The wizard takes you back to the **Rule groups** page where your new rule group is listed\.

You now have a rule group that allows only specific domain queries through\. To begin using it, you associate it with the VPCs where you want to use the filtering behavior\.