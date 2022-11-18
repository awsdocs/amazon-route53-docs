# Working with private hosted zones<a name="hosted-zones-private"></a>

A *private hosted zone* is a container that holds information about how you want Amazon Route 53 to respond to DNS queries for a domain and its subdomains within one or more VPCs that you create with the Amazon VPC service\. Here's how private hosted zones work:

1. You create a private hosted zone, such as example\.com, and specify the VPC that you want to associate with the hosted zone\. After you create the hosted zone you can associate more VPCs with it\.

1. You create records in the hosted zone that determine how Route 53 responds to DNS queries for your domain and subdomains within and among your VPCs\. For example, suppose you have a database server that runs on an EC2 instance in the VPC that you associated with your private hosted zone\. You create an A or AAAA record, such as db\.example\.com, and you specify the IP address of the database server\. 

   For more information about records, see [Working with records](rrsets-working-with.md)\. For information about the Amazon VPC requirements for using private hosted zones, see [Using private hosted zones](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-dns.html#vpc-private-hosted-zones) in the *Amazon VPC User Guide*\.

1. When an application submits a DNS query for db\.example\.com, Route 53 returns the corresponding IP address\. To get an answer from a private hosted zone you also have to be running an EC2 instance in one of the associated VPCs \(or have an inbound endpoint from a hybrid setup\.\) If you try to query a private hosted zone from outside the VPCs or your hybrid setup, the query will be recursively resolved on the internet\.

1. The application uses the IP address that it got from Route 53 to establish a connection with the database server\.

When you create a private hosted zone, the following name servers are used:
+ ns\-0\.awsdns\-00\.com
+ ns\-512\.awsdns\-00\.net
+ ns\-1024\.awsdns\-00\.org
+ ns\-1536\.awsdns\-00\.co\.uk

These name servers are used because the DNS protocol requires that every hosted zone must have an NS record set\. These name servers are reserved and never used by Route 53 public hosted zones\. You can only query those zones via Route 53 Resolver in a VPC that has been associated to the hosted zone by using an inbound endpoint connected to the VPCs specified in the private hosted zone\.

 While the name servers are visible on the internet, Route 53 Resolver doesn't connect to the name server addresses\. Further, the private hosted zone information is not returned if you directly query the name servers over the internet\. Instead, the Route 53 Resolver detects that queries are within a private namespace based on VPC to hosted zone associations and uses direct, private connectivity to reach the private DNS servers\.

**Note**  
You can change the NS record set in a private hosted zone if you want and private DNS resolution will still work\. We don't recommend doing so, but if you choose to, you should use reserved domain names which are not used by public DNS servers\.

If you want to route traffic for your domain on the internet, you use a Route 53 *public* hosted zone\. For more information, see [Working with public hosted zones](AboutHZWorkingWith.md)\.

**Topics**
+ [Considerations when working with a private hosted zone](hosted-zone-private-considerations.md)
+ [Creating a private hosted zone](hosted-zone-private-creating.md)
+ [Listing private hosted zones](hosted-zone-private-listing.md)
+ [Associating more VPCs with a private hosted zone](hosted-zone-private-associate-vpcs.md)
+ [Associating an Amazon VPC and a private hosted zone that you created with different AWS accounts](hosted-zone-private-associate-vpcs-different-accounts.md)
+ [Disassociating VPCs from a private hosted zone](hosted-zone-private-disassociate-vpcs.md)
+ [Deleting a private hosted zone](hosted-zone-private-deleting.md)