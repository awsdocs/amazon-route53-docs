# Replacing the Hosted Zone for a Domain That Is Registered with Route 53<a name="domain-replace-hosted-zone"></a>

If you [delete the hosted zone](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/DeleteHostedZone.html) for a domain, you need to create another hosted zone when you're ready to make the domain available on the internet\. Perform the following procedure\.

**To replace the hosted zone for a domain**

1. Create a public hosted zone\. For more information, see [Creating a Public Hosted Zone](CreatingHostedZone.md)\.

1. Create records in the hosted zone\. Records define how you want to route traffic for the domain \(example\.com\) and subdomains \(acme\.example\.com, zenith\.example\.com\)\. For more information, see [Working with Records](rrsets-working-with.md)\.

1. Update the domain configuration to use the name servers for the new hosted zone\. For more information, see [Adding or Changing Name Servers and Glue Records for a Domain](domain-name-servers-glue-records.md)\.
**Important**  
When you create a hosted zone, Route 53 assigns a set of four name servers to the hosted zone\. If you delete a hosted zone and then create a new one, Route 53 assigns another set of four name servers\. Typically, none of the name servers for the new hosted zone match any of the name servers for the previous hosted zone\. If you don't update the domain configuration to use the name servers for the new hosted zone, the domain will remain unavailable on the internet\.

1. If you encounter issues while replacing the hosted zone for a domain, you can contact customer support for free\. For more information, see [Contacting Customer Support About Domain Registration Issues](domain-contact-support.md)\.