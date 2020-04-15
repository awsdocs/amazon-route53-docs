# Disassociating VPCs from a private hosted zone<a name="hosted-zone-private-disassociate-vpcs"></a>

You can use the Amazon Route 53 console to disassociate VPCs from a private hosted zone\. This causes Route 53 to stop routing traffic using records in the hosted zone for DNS queries that originate in the VPC\. For example, if the example\.com hosted zone is associated with a VPC and you disassociate the hosted zone from that VPC, Route 53 stops resolving DNS queries for example\.com or any of the other records in the example\.com hosted zone\. 

**Note**  
You can't disassociate the last VPC from a private hosted zone\. If you want to disassociate that VPC, you must first associate another VPC with the hosted zone\.

**To disassociate VPCs from a private hosted zone**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the private hosted zone that you want to disassociate one or more VPCs from\.

1. In the right pane, choose the **x** icon next to the VPC that you want to disassociate from this hosted zone\.

1. Choose **Disassociate** to confirm\.