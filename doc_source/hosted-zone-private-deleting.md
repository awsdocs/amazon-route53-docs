# Deleting a Private Hosted Zone<a name="hosted-zone-private-deleting"></a>

The following procedure explains how to delete a private hosted zone using the Amazon Route 53 console\. For information about how to delete a private hosted zone using the Route 53 API, see [DeleteHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHostedZone.html) in the *Amazon Route 53 API Reference*\. 

You can delete a private hosted zone only if there are no records other than the default SOA and NS records\. If your hosted zone contains other records, you must delete them before you can delete your hosted zone\. This prevents you from accidentally deleting a hosted zone that still contains records\.

**To delete a private hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Confirm that the hosted zone that you want to delete contains only an NS and an SOA record\. If it contains additional records, delete them:

   1. Choose the name of the hosted zone that you want to delete\.

   1. On the Record Sets page, if the list of records includes any records for which the value of the **Type** column is something other than **NS** or **SOA**, choose the row, and choose **Delete Record Set**\.

      To select multiple, consecutive records, choose the first row, press and hold the **Shift** key, and choose the last row\. To select multiple, non\-consecutive records, choose the first row, press and hold the **Ctrl** key, and choose the remaining rows\. 

   1. Choose **Back to Hosted Zones**\.

1. On the Hosted Zones page, choose the row for the hosted zone that you want to delete\.

1. Choose **Delete Hosted Zone**\.

1. Choose **Confirm**\.