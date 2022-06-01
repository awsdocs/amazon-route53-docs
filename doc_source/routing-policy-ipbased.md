# IP\-based routing<a name="routing-policy-ipbased"></a>

With IP\-based routing in Amazon Route 53, you can fine\-tune your DNS routing by using your understanding of your network, applications, and clients to make the best DNS routing decisions for your end users\. IP\-based routing gives you granular control to optimize performance or reduce network costs by uploading your data to Route 53 in the form of user\-IP\-to\-endpoint mappings\.

Geolocation and latency\-based routing is based on data that Route 53 collects and keeps up to date\. This approach works well for the majority of customers, but IP\-based routing offers you the additional ability to optimize routing based on specific knowledge of your customer base\. For example, a global video content provider may want to route end users from a particular Internet Service\.

Some common use cases for IP\-based routing are as follows:
+ You want to route end users from certain ISPs to specific endpoints in order to optimize network transit costs or performance\.
+ You want to add overrides to existing Route 53 routing types such as geolocation routing based on your knowledge of your clients' physical locations\.

**Managing IP ranges and associating them to a resource record set \(RRSet\)**  
You can specify CIDR blocks from /0 to /24 for IPv4 and 0 to /48 for IPv6\. For example, a /24 IPv4 CIDR block includes 256 contiguous IP addresses\. You can group sets of CIDR blocks \(or IP ranges\) into CIDR locations, which are in turn grouped into reusable entities called CIDR collections: 

**CIDR block**  
An IP range in CIDR notation, for example, 192\.0\.2\.0/24 or 2001:DB8::/32\.

**CIDR location**  
A named list of CIDR blocks\. For example, example\-isp\-seattle = \[192\.0\.2\.0/24, 203\.0\.113\.0/22, 198\.51\.100\.0/24, 2001:DB8::/32 \]\. The blocks in a CIDR location list don't have to be adjacent or the same range\.   
A single location can have both IPv4 and IPv6 blocks and this location can be associated to both A and AAAA record sets respectively\.   
The location name is often a location by convention, but can be any string, for example *Company\-A*\.

**CIDR collection**  
A named collection of locations\. For example, mycollection = \[example\-isp\-seattle, example\-isp\-tokyo\]\.  
IP\-based routing resource record sets reference a location in a collection, and all resource record sets for the same record set name and type must reference the same collection\. For example, if you create websites in two regions and want to direct DNS queries from two different CIDR locations to a specific website based on the originating IP addresses, then both of those locations must be listed in the same CIDR collection\.  
You can also share these collections across AWS accounts using AWS RAM\. When you make an update, such as editing one of the IP ranges in a collection, this update will automatically apply to all the record sets associated with the collection

For information about values that you specify when you use the IP\-based routing policy to create records, see the following topics:
+ [Values specific for IP\-based records](resource-record-sets-values-ipbased.md)
+ [Values specific for IP\-based alias records](resource-record-sets-values-ipbased-alias.md)
+ [Values that are common for all routing policies](resource-record-sets-values-shared.md)
+ [Values that are common for alias records for all routing policies](resource-record-sets-values-alias-common.md)

**Topics**
+ [Creating a CIDR collection with CIDR locations and blocks](resource-record-sets-creating-cidr-collection.md)
+ [Working with CIDR locations and blocks](resource-record-sets-working-with-cidr-locations.md)
+ [Deleting a CIDR collection](resource-record-sets-delete-cidr-collection.md)
+ [Moving a geolocation to IP\-based routing](resource-record-sets-move-geolocation-to-cidr.md)