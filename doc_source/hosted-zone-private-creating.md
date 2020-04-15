# Creating a private hosted zone<a name="hosted-zone-private-creating"></a>

A private hosted zone is a container for records for a domain that you host in one or more Amazon virtual private clouds \(VPCs\)\. You create a hosted zone for a domain \(such as example\.com\), and then you create records to tell Amazon Route 53 how you want traffic to be routed for that domain within and among your VPCs\.

**Important**  
When you create a private hosted zone, you must associate a VPC with the hosted zone, and the VPC that you specify must have been created by using the same account that you're using to create the hosted zone\. After you create the hosted zone, you can associate additional VPCs with it, including VPCs that you created by using a different AWS account\.  
To associate VPCs that you created by using one account with a private hosted zone that you created by using a different account, you must authorize the association and then make the association programmatically\. For more information, see [Associating an Amazon VPC and a private hosted zone that you created with different AWS accounts](hosted-zone-private-associate-vpcs-different-accounts.md)\.

For information about creating a private hosted zone by using the Route 53 API, see the [Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/)\.

**To create a private hosted zone using the Route 53 console**

1. For each VPC that you want to associate with the Route 53 hosted zone, change the following VPC settings to `true`:
   + `enableDnsHostnames`
   + `enableDnsSupport`

   For more information, see [Updating DNS support for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-dns-updating) in the *Amazon VPC User Guide*\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Route 53, choose **Hosted Zones** in the navigation pane\.

1. Choose **Create Hosted Zone**\.

1. In the **Create Private Hosted Zone** pane, enter a domain name and, optionally, a comment\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

1. In the **Type** list, choose **Private Hosted Zone for Amazon VPC**\.

1. In the **VPC ID** list, choose the VPC that you want to associate with the hosted zone\.

   If you want to associate more than one VPC with the hosted zone, you can add VPCs after you create the hosted zone\.
**Note**  
If the console displays the following message, you're trying to associate a VPC with this hosted zone that has already been associated with another hosted zone that has an overlapping name space, such as example\.com and retail\.example\.com:  
"A conflicting domain is already associated with the given VPC or Delegation Set\."

1. Choose **Create**\.

1. To associate more VPCs with the new hosted zone, perform the following steps:

   1. Choose **Back to Hosted Zones**\.

   1. Choose the radio button for the hosted zone\.

   1. In the right pane, in **VPC ID**, choose another VPC that you want to associate with the hosted zone\.

   1. Choose **Associate New VPC**\.

   1. Repeat steps c and d until you have associated all of the VPCs that you want to with the hosted zone\.