# Associating more VPCs with a private hosted zone<a name="hosted-zone-private-associate-vpcs"></a>

You can use the Amazon Route 53 console to associate more VPCs with a private hosted zone if you created the hosted zone and the VPCs by using the same AWS account\.

**Important**  
If you want to associate VPCs that you created by using one account with a private hosted zone that you created by using a different account, you first must authorize the association\. In addition, you can't use the AWS console either to authorize the association or associate the VPCs with the hosted zone\. For more information, see [Associating an Amazon VPC and a private hosted zone that you created with different AWS accounts](hosted-zone-private-associate-vpcs-different-accounts.md)\.

For information about how to associate more VPCs with a private hosted zone using the Route 53 API, see [AssociateVPCWithHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_AssociateVPCWithHostedZone.html) in the *Amazon Route 53 API Reference*\.

**To associate additional VPCs with a private hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the radio button for the private hosted zone that you want to associate more VPCs with\.

1. In the right pane, in **VPC ID**, choose the ID of the VPC that you want to associate with this hosted zone\.

1. Choose **Associate New VPC**\.

1. To associate more VPCs with this hosted zone, repeat steps 4 and 5\.