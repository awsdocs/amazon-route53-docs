# Listing Resource Record Sets<a name="resource-record-sets-listing"></a>

The following procedure explains how to use the Amazon Route 53 console to list the resource record sets in a hosted zone\. For information about how to list resource record sets using the Amazon Route 53 API, see [ListResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListResourceRecordSets.html) in the *Amazon Route 53 API Reference*\. 

**To list resource record sets**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. On the **Hosted Zones** page, double\-click the name of a hosted zone to see its Record Sets page\.

   To display only selected resource record sets, enter the applicable search criteria above the list of resource record sets:

   + To display the resource record sets that have specific values in either the **Name** or **Value** field, enter a value in the **Search** field\. For example, to display the resource record sets that have an IP address beginning with **192\.0**, type that value in the **Search** field\.

   + To display only the resource record sets that have the same DNS record type, select the type in the drop down list\. 

   + To display only alias resource record sets, select **Aliases Only**\.

   + To display only weighted resource record sets, select **Weighted Only**\.