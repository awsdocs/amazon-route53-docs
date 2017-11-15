# Working with Public Hosted Zones<a name="AboutHZWorkingWith"></a>

A public hosted zone is a container that holds information about how you want to route traffic on the internet for a domain, such as example\.com, and its subdomains \(apex\.example\.com, acme\.example\.com\)\. After you create a public hosted zone, you create resource record sets that determine how the Domain Name System \(DNS\) responds to queries for your domain and subdomains\. For example, if you have one or more email addresses associated with your domain \(john@example\.com\), you'll create an MX record in your hosted zone so that email is sent to the email server for your domain\. For more information about resource record sets, see [Working with Resource Record Sets](rrsets-working-with.md)\.

This topic explains how to use the Amazon Route 53 console to create, list, and delete public hosted zones\. For information about using the Amazon Route 53 API to perform these operations, see the [Amazon Route 53 API Reference](http://docs.aws.amazon.com/Route53/latest/APIReference/)\.

You can also use an Amazon Route 53 *private* hosted zone to route traffic within one or more Amazon Virtual Private Clouds\. For more information, see [Working with Private Hosted Zones](hosted-zones-private.md)\.


+ [Creating a Public Hosted Zone](CreatingHostedZone.md)
+ [Getting the Name Servers for a Public Hosted Zone](GetInfoAboutHostedZone.md)
+ [Listing Public Hosted Zones](ListInfoOnHostedZone.md)
+ [Deleting a Public Hosted Zone](DeleteHostedZone.md)
+ [Checking DNS Responses from Amazon Route 53](dns-test.md)
+ [Configuring White Label Name Servers](white-label-name-servers.md)
+ [NS and SOA Resource Record Sets that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)