# Editing records<a name="resource-record-sets-editing"></a>

The following procedure explains how to edit records using the Amazon Route 53 console\. For information about how to edit records using the Route 53 API, see [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

**Note**  
Your changes to records take time to propagate to the Route 53 DNS servers\. Currently, the only way to verify that changes have propagated is to use the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API action\. Changes generally propagate to all Route 53 name servers within 60 seconds\.<a name="resource-record-sets-editing-procedure"></a>

**To edit records using the Route 53 console**

1. If you're not editing alias records, skip to step 2\. 

   If you're editing alias records that route traffic to ELB Classic, Application, or Network Load Balancers, and if you created your Route 53 hosted zone and your load balancer using different accounts, perform the procedure [Getting the DNS name for an ELB load balancer](resource-record-sets-creating.md#resource-record-sets-elb-dns-name-procedure) to get the DNS name for the load balancer\. 

   If you're editing alias records for any other AWS resource, skip to step 2\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. On the **Hosted Zones** page, choose the row for the hosted zone that contains the records that you want to edit\.

1. Choose the row for the record that you want to edit\. 

1. Enter the applicable values\. For more information, see [Values that you specify when you create or edit Amazon Route 53 records](resource-record-sets-values.md)\. 

1. Choose **Save Record Set**\.

1. If you're editing multiple records, repeat steps 5 through 7\.