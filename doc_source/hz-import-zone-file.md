# Import zone file<a name="hz-import-zone-file"></a>

You can create up to 1000 records at a time by importing a zone file in Bind format\. Paste the contents of your zone file in the **Zone file** field\. 

In the **Record preview for domain\-name** field, review the records that Route 53 will create when you choose **Import**\. If you change the content of the **Zone file** field, the **Record preview for domain\-name** field is updated to show the changes\.

You can import records as many times as you want\. There's a quota on the number of records in a hosted zone, but you can request to have the quota increased\. See [Quotas on records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/DNSLimitations.html#limits-api-entities-records)\.

## Learn more<a name="hz-import-learn-more"></a>
+ [Creating records by importing a zone file](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-creating-import.html)