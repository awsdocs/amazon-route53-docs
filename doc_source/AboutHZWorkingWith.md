# Working with Public Hosted Zones<a name="AboutHZWorkingWith"></a>

A public hosted zone is a container that holds information about how you want to route traffic on the internet for a specific domain, such as example\.com, and its subdomains \(apex\.example\.com, acme\.example\.com\)\. You get a public hosted zone in one of two ways:

+ When you register a domain with Route 53, we create a hosted zone for you automatically\.

+ When you transfer DNS service for an existing domain to Route 53, you start by creating a hosted zone for the domain\. For more information, see [Making Amazon Route 53 the DNS Service for an Existing DomainMaking Route 53 the DNS Service for an Existing Domain](MigratingDNS.md)\.

In both cases, you then create records in the hosted zone to specify how you want to route traffic for the domain and subdomains\. For example, you might create a record to route traffic for www\.example\.com to a CloudFront distribution or to a web server in your data center\. For more information about records, see [Working with Records](rrsets-working-with.md)\.

This topic explains how to use the Amazon Route 53 console to create, list, and delete public hosted zones\. 

**Note**  
You can also use a Route 53 *private* hosted zone to route traffic within one or more VPCs that you create with the Amazon VPC service\. For more information, see [Working with Private Hosted Zones](hosted-zones-private.md)\.


+ [Considerations When Working with Public Hosted Zones](hosted-zone-public-considerations.md)
+ [Creating a Public Hosted Zone](CreatingHostedZone.md)
+ [Getting the Name Servers for a Public Hosted Zone](GetInfoAboutHostedZone.md)
+ [Listing Public Hosted Zones](ListInfoOnHostedZone.md)
+ [Deleting a Public Hosted Zone](DeleteHostedZone.md)
+ [Checking DNS Responses from Route 53](dns-test.md)
+ [Configuring White\-Label Name Servers](white-label-name-servers.md)
+ [NS and SOA Records that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)