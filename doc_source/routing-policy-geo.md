# Geolocation routing<a name="routing-policy-geo"></a>

Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from\. For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region\. 

When you use geolocation routing, you can localize your content and present some or all of your website in the language of your users\. You can also use geolocation routing to restrict distribution of content to only the locations in which you have distribution rights\. Another possible use is for balancing load across endpoints in a predictable, easy\-to\-manage way, so that each user location is consistently routed to the same endpoint\. 

You can specify geographic locations by continent, by country, or by state in the United States\. If you create separate records for overlapping geographic regions—for example, one record for North America and one for Canada—priority goes to the smallest geographic region\. This allows you to route some queries for a continent to one resource and to route queries for selected countries on that continent to a different resource\. \(For a list of the countries on each continent, see [Location](resource-record-sets-values-geo.md#rrsets-values-geo-location)\.\)

Geolocation works by mapping IP addresses to locations\. However, some IP addresses aren't mapped to geographic locations, so even if you create geolocation records that cover all seven continents, Amazon Route 53 will receive some DNS queries from locations that it can't identify\. You can create a default record that handles both queries from IP addresses that aren't mapped to any location and queries that come from locations that you haven't created geolocation records for\. If you don't create a default record, Route 53 returns a "no answer" response for queries from those locations\.

For more information, see [How Amazon Route 53 uses EDNS0 to estimate the location of a user](routing-policy-edns0.md)\.

For information about values that you specify when you use the geolocation routing policy to create records, see the following topics:
+ [Values specific for geolocation records](resource-record-sets-values-geo.md)
+ [Values specific for geolocation alias records](resource-record-sets-values-geo-alias.md)
+ [Values that are common for all routing policies](resource-record-sets-values-shared.md)
+ [Values that are common for alias records for all routing policies](resource-record-sets-values-alias-common.md)