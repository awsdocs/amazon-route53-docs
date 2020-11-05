# Hosted zone details<a name="hz-details"></a>

The details page for a hosted zone include the following information:
+ **Hosted zone ID**: Route 53 assigns the ID when you create a hosted zone\. The main use for this ID is programmatic access to the hosted zone\.
+ **Description**: In the list of hosted zones, this value lets you distinguish hosted zones that have the same name\. A description is optional\. 
+ **Type**: The type specifies whether this is a public hosted zone \(for routing traffic on the internet\) or a private hosted zone \(for routing traffic within and among VPCs\)\. 
+ **Name servers**: Route 53 assigns name servers when you create a hosted zone\. The assigned name servers can't be changed\. 

  To make Route 53 the DNS service for a domain \(to use the records in a public hosted zone to route traffic on the internet for a domain\), you update the domain registration to use these name servers\.
+ **Record count**: The total number of records in a hosted zone, including the default NS and SOA records\.

## Learn more<a name="hz-details-learn-more"></a>
+ [Making Route 53 the DNS service for an existing domain](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/MigratingDNS.html)