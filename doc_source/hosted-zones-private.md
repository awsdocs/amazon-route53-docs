# Working with Private Hosted Zones<a name="hosted-zones-private"></a>

A private hosted zone is a container that holds information about how you want to route traffic for a domain and its subdomains within one or more Amazon Virtual Private Clouds \(Amazon VPCs\)\. To begin, you create a private hosted zone and specify the Amazon VPCs that you want to associate with the hosted zone\. You then create records that determine how Amazon Route 53 responds to queries for your domain and subdomains within and among your Amazon VPCs\. Resources within your associated VPC will be permitted to resolve records existing in the private hosted zone\. For example, if you have webserver\.example\.com, you'll create an A record in your private hosted zone so browser queries from resources inside the associated VPC can resolve your web server's IP address\. For more information about records, see [Working with Records](rrsets-working-with.md)\. For information about the Amazon VPC requirements for using private hosted zones, see [Using Private Hosted Zones](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html#vpc-private-hosted-zones) in the *Amazon VPC User Guide*\.

If you want to route traffic for your domain on the internet, you use a Route 53 *public* hosted zone\. For more information, see [Working with Public Hosted Zones](AboutHZWorkingWith.md)\.


+ [Considerations When Working with a Private Hosted Zone](hosted-zone-private-considerations.md)
+ [Creating a Private Hosted Zone](hosted-zone-private-creating.md)
+ [Listing Private Hosted Zones](hosted-zone-private-listing.md)
+ [Associating More Amazon VPCs with a Private Hosted Zone](hosted-zone-private-associate-vpcs.md)
+ [Associating an Amazon VPC and a Private Hosted Zone That You Created with Different AWS Accounts](hosted-zone-private-associate-vpcs-different-accounts.md)
+ [Disassociating Amazon VPCs from a Private Hosted Zone](hosted-zone-private-disassociate-vpcs.md)
+ [Deleting a Private Hosted Zone](hosted-zone-private-deleting.md)
