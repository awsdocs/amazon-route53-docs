# Listing records<a name="resource-record-sets-listing"></a>

The following procedure explains how to use the Amazon Route 53 console to list the records in a hosted zone\. For information about how to list records using the Route 53 API, see [ListResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListResourceRecordSets.html) in the *Amazon Route 53 API Reference*\. 

**To list records**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. On the **Hosted Zones** page, choose the name of a hosted zone\.

   To display only selected records, enter the applicable search criteria above the list of records\. Search behavior depends on whether the hosted zone contains up to 2,000 records or more than 2,000 records:  
**Up to 2,000 records**  
   + To display the records that have specific values in either the **Name** or **Value** field, enter a value in the **Search** field and press **Enter**\. For example, to display the records that have an IP address beginning with **192\.0**, enter that value in the **Search** field and press **Enter**\.
   + To display only the records that have the same DNS record type, select the type in the dropdown list\. 
   + To display only alias records, select the **Aliases Only** check box\.
   + To display only weighted records, select the **Weighted Only** check box\.  
**More than 2,000 records**  
   + You can search only on record names, not on record values\. You also can't filter based on the record type, or on alias or weighted records\.
   + For records that have three labels \(three parts separated by dots\), when you enter a value in the search field and press **Enter**, the Route 53 console automatically performs a wildcard search on the third label from the right in the record name\. For example, suppose the hosted zone example\.com contains 100 records named record1\.example\.com through record100\.example\.com\. \(Record1 is the third label from the right\.\) Here's what happens when you search on the following values:
     + **record1** – The Route 53 console searches for **record1\*\.example\.com**, which returns **record1\.example\.com**, **record10\.example\.com** through **record19\.example\.com**, and **record100\.example\.com**\.
     + **record1\.example\.com** – As in the preceding example, the console searches for **record1\*\.example\.com** and returns the same records\.
     + **1** – The console searches for **1\*\.example\.com** and returns no records\.
     + **example** – The console searches for **example\*\.example\.com** and returns no records\.
     + **example\.com** – In this example, the console doesn't perform a wildcard search\. It returns all the records in the hosted zone\.
**Note**  
If the third label from the right contains one or more hyphens \(such as `third-label.example.com`\), and if you search for the part of the third label immediately before the hyphen \(`third` in this example\), Route 53 won't return any records\. Instead, either include the hyphen \(search for `third-`\) or omit the character immediately before the hyphen \(search for `thir`\)\.
   + For records that have four or more labels, you must specify the exact name of the record\. No wildcard searches are supported\. For example, if the hosted zone includes a record named label4\.record1\.example\.com, you can find that record only if you specify **label4\.record1\.example\.com** in the search field\.