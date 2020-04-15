# Working with private hosted zones<a name="hosted-zones-private"></a>

A *private hosted zone* is a container that holds information about how you want Amazon Route 53 to respond to DNS queries for a domain and its subdomains within one or more VPCs that you create with the Amazon VPC service\. Here's how private hosted zones work:

1. You create a private hosted zone, such as example\.com, and specify the VPCs that you want to associate with the hosted zone\.

1. You create records in the hosted zone that determine how Route 53 responds to DNS queries for your domain and subdomains within and among your VPCs\. For example, suppose you have a database server that runs on an EC2 instance in one of the VPCs that you associated with your private hosted zone\. You create an A or AAAA record, such as db\.example\.com, and you specify the IP address of the database server\. 

   For more information about records, see [Working with records](rrsets-working-with.md)\. For information about the Amazon VPC requirements for using private hosted zones, see [Using private hosted zones](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-private-hosted-zones) in the *Amazon VPC User Guide*\.

1. When an application submits a DNS query for db\.example\.com, Route 53 returns the corresponding IP address\. The application must also be running on an EC2 instance in one of the VPCs that you associated with the example\.com private hosted zone\.

1. The application uses the IP address that it got from Route 53 to establish a connection with the database server\.

If you want to route traffic for your domain on the internet, you use a Route 53 *public* hosted zone\. For more information, see [Working with public hosted zones](AboutHZWorkingWith.md)\.

**Topics**
+ [Considerations when working with a private hosted zone](hosted-zone-private-considerations.md)
+ [Creating a private hosted zone](hosted-zone-private-creating.md)
+ [Listing private hosted zones](hosted-zone-private-listing.md)
+ [Associating more VPCs with a private hosted zone](hosted-zone-private-associate-vpcs.md)
+ [Associating an Amazon VPC and a private hosted zone that you created with different AWS accounts](hosted-zone-private-associate-vpcs-different-accounts.md)
+ [Disassociating VPCs from a private hosted zone](hosted-zone-private-disassociate-vpcs.md)
+ [Deleting a private hosted zone](hosted-zone-private-deleting.md)