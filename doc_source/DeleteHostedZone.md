# Deleting a Public Hosted Zone<a name="DeleteHostedZone"></a>

The following procedure explains how to delete a hosted zone using the Amazon Route 53 console\. For information about how to delete a hosted zone using the Amazon Route 53 API, see [DeleteHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHostedZone.html) in the *Amazon Route 53 API Reference*\. 

**Important**  
If the name servers for the hosted zone are associated with a domain and if you want to make the domain unavailable on the internet, we recommend that you delete the name servers from the domain to prevent future DNS queries from possibly being misrouted\. If the domain is registered with Amazon Route 53, see [Adding or Changing Name Servers and Glue Records for a Domain](domain-name-servers-glue-records.md)\. If the domain is registered with another registrar, use the method provided by the registrar to delete name servers for the domain\.  
Some domain registries don't allow you to remove all of the name servers for a domain\. If the registry for your domain requires one or more name servers, we recommend that you delete the hosted zone only if you transfer DNS service to another service provider, and you replace the name servers for the domain with name servers from the new provider\. 

You can delete a hosted zone only if there are no resource record sets other than the default SOA and NS records\. If your hosted zone contains other resource record sets, you must delete them before you can delete your hosted zone\. This prevents you from accidentally deleting a hosted zone that still contains resource record sets\.

**To delete a public hosted zone using the Amazon Route 53 console**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Confirm that the hosted zone that you want to delete contains only an NS and an SOA resource record set\. If it contains additional resource record sets, delete them:

   1. Choose the name of the hosted zone that you want to delete\.

   1. On the Record Sets page, if the list of resource record sets includes any resource record sets for which the value of the **Type** column is something other than NS or SOA, choose the row, and choose **Delete Record Set**\.

      To select multiple, consecutive resource record sets, choose the first row, press and hold the **Shift** key, and choose the last row\. To select multiple, non\-consecutive resource record sets, choose the first row, press and hold the **Ctrl** key, and choose the remaining rows\. 
**Note**  
If you created any NS records for subdomains in the hosted zone, delete those records, too\.

   1. Choose **Back to Hosted Zones**\.

1. On the **Hosted Zones** page, choose the row for the hosted zone that you want to delete\.

1. Choose **Delete Hosted Zone**\.

1. Choose **OK** to confirm\.

1. If you want to make the domain unavailable on the internet, we recommend that you delete the name servers from the domain to prevent future DNS queries from possibly being misrouted\.

   If the domain is registered with Amazon Route 53, see [Adding or Changing Name Servers and Glue Records for a Domain](domain-name-servers-glue-records.md)\. If the domain is registered with another registrar, use the method provided by the registrar to delete name servers for the domain\.