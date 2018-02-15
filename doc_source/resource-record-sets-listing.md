# Listing Records<a name="resource-record-sets-listing"></a>

The following procedure explains how to use the Amazon Route 53 console to list the records in a hosted zone\. For information about how to list records using the Route 53 API, see [ListResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListResourceRecordSets.html) in the *Amazon Route 53 API Reference*\. 

**To list records**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. On the **Hosted Zones** page, double\-click the name of a hosted zone to see its Record Sets page\.

   To display only selected records, enter the applicable search criteria above the list of records:

   + To display the records that have specific values in either the **Name** or **Value** field, enter a value in the **Search** field and press **Enter**\. For example, to display the records that have an IP address beginning with **192\.0**, type that value in the **Search** field and press **Enter**\.
**Note**  
If a hosted zone contains more than 2,000 records, you can search only by the name of the record, not by values in the **Value** field\.

   + To display only the records that have the same DNS record type, select the type in the drop down list\. 

   + To display only alias records, select **Aliases Only**\.

   + To display only weighted records, select **Weighted Only**\.