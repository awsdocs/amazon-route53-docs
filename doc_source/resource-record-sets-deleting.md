# Deleting Resource Record Sets<a name="resource-record-sets-deleting"></a>

The following procedure explains how to delete resource record sets using the Amazon Route 53 console\. For information about how to delete resource record sets using the Amazon Route 53 API, see [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

**Note**  
Your changes to resource record sets take time to propagate to the Amazon Route 53 DNS servers\. Currently, the only way to verify that changes have propagated is to use the [GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API action\. Changes generally propagate to all Amazon Route 53 name servers within 60 seconds\.

**To delete resource record sets**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. On the Hosted Zones page, double\-click the row for the hosted zone that contains resource record sets that you want to delete\. 

1. In the list of resource record sets, select the resource record set that you want to delete\.

   To select multiple, consecutive resource record sets, click the first row, hold the **Shift** key, and click the last row\. To select multiple, nonconsecutive resource record sets, click the first row, hold the **Ctrl** key, and click additional rows\. 

   You cannot delete the resource record sets that have a value of **NS** or **SOA** for **Type**\.

1. Click **Delete Record Set**\.

1. Click **OK** to confirm\.