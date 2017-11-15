# Choosing a Routing Policy<a name="routing-policy"></a>

When you create a resource record set, you choose a routing policy, which determines how Amazon Route 53 responds to queries: 

+ **Simple routing policy** – Use for a single resource that performs a given function for your domain, for example, a web server that serves content for the example\.com website\.

+ **Failover routing policy** – Use when you want to configure active\-passive failover\. 

+ **Geolocation routing policy** – Use when you want to route traffic based on the location of your users\.

+ **Geoproximity routing policy** – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from one resources in one location to resources in another\.

+ **Latency routing policy** – Use when you have resources in multiple locations and you want to route traffic to the resource that provides the best latency\.

+ **Multivalue answer routing policy** – Use when you want Amazon Route 53 to respond to DNS queries with up to eight healthy records selected at random\.

+ **Weighted routing policy** – Use to route traffic to multiple resources in proportions that you specify\.


+ [Failover Routing](#routing-policy-failover)
+ [Geolocation Routing](#routing-policy-geo)
+ [Geoproximity Routing \(Traffic Flow Only\)](#routing-policy-geoproximity)
+ [Latency\-based Routing](#routing-policy-latency)
+ [Multivalue Answer Routing](#routing-policy-multivalue)
+ [Weighted Routing](#routing-policy-weighted)

## Failover Routing<a name="routing-policy-failover"></a>

Failover routing lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy\. The primary and secondary resource record sets can route traffic to anything from an Amazon S3 bucket that is configured as a website to a complex tree of records\. For more information, see [Configuring Active\-Passive Failover by Using Amazon Route 53 Failover and Failover Alias Records](dns-failover-configuring-options.md#dns-failover-failover-rrsets) and [Configuring Failover in a Private Hosted Zone](dns-failover-private-hosted-zones.md)\. 

## Geolocation Routing<a name="routing-policy-geo"></a>

Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from\. For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region\. 

When you use geolocation routing, you can localize your content and present some or all of your website in the language of your users\. You can also use geolocation routing to restrict distribution of content to only the locations in which you have distribution rights\. Another possible use is for balancing load across endpoints in a predictable, easy\-to\-manage way, so that each user location is consistently routed to the same endpoint\. 

You can specify geographic locations by continent, by country, or by state in the United States\. If you create separate records for overlapping geographic regions—for example, one record for North America and one for Canada—priority goes to the smallest geographic region\. This allows you to route some queries for a continent to one resource and to route queries for selected countries on that continent to a different resource\. \(For a list of the countries on each continent, see [Location](resource-record-sets-values-geo.md#rrsets-values-geo-location)\.\)

Geolocation works by mapping IP addresses to locations\. However, some IP addresses aren't mapped to geographic locations, so even if you create geolocation resource record sets that cover all seven continents, Amazon Route 53 will receive some DNS queries from locations that it can't identify\. You can create a default record that handles both queries from IP addresses that aren't mapped to any location and queries that come from locations that you haven't created geolocation records for\. If you don't create a default record, Amazon Route 53 returns a "no answer" response for queries from those locations\.

To improve the accuracy of geolocation routing, Amazon Route 53 supports the edns\-client\-subnet extension of EDNS0\. \(EDNS0 adds several optional extensions to the DNS protocol\.\) Amazon Route 53 can use edns\-client\-subnet only when DNS resolvers support it:

+ When a browser or other viewer uses a DNS resolver that does not support edns\-client\-subnet, Amazon Route 53 uses the source IP address of the DNS resolver to approximate the location of the user and responds to geolocation queries with the DNS record for the resolver's location\.

+ When a browser or other viewer uses a DNS resolver that does support edns\-client\-subnet, the DNS resolver sends Amazon Route 53 a truncated version of the user's IP address\. Amazon Route 53 determines the location of the user based on the truncated IP address rather than the source IP address of the DNS resolver; this typically provides a more accurate estimate of the user's location\. Amazon Route 53 then responds to geolocation queries with the DNS record for the user's location\.

For more information about edns\-client\-subnet, see the IETF draft [Client Subnet in DNS Requests](http://tools.ietf.org/html/draft-vandergaast-edns-client-subnet-02)\.

## Geoproximity Routing \(Traffic Flow Only\)<a name="routing-policy-geoproximity"></a>

Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your resources\. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a *bias*, that expands or shrinks the size of the geographic region from which traffic is routed to a resource\.

To use geoproximity routing, you must use Amazon Route 53 [traffic flow](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/traffic-flow.html)\. You create geoproximity rules for your resources and specify one of the following values for each rule:

+ If you're using AWS resources, the AWS Region that you created the resource in

+ If you're using non\-AWS resources, the latitude and longitude of the resource

To optionally expand the size of the geographic region from which Amazon Route 53 routes traffic to a resource, specify a positive integer from 1 to 99 for the bias\. Amazon Route 53 shrinks the size of adjacent regions\. When you specify a negative bias of \-1 to \-99, the opposite is true\. The effect of changing the bias for your resources depends on a number of factors, including the following:

+ The number of resources that you have\.

+ How close the resources are to one another\.

+ The number of users that you have near the border area between geographic regions\. For example, if you have resources in Boston and Washington, DC and you have a lot of users in New York City, which is roughly equidistant between your resources, a small change in bias could result in a large swing in traffic from resources in Boston to resources in DC or vice versa\.

We recommend that you change the bias in small increments to prevent overwhelming your resources due to an unanticipated swing in traffic\.

## Latency\-based Routing<a name="routing-policy-latency"></a>

If your application is hosted in multiple Amazon EC2 regions, you can improve performance for your users by serving their requests from the Amazon EC2 region that provides the lowest latency\. 

To use latency\-based routing, you create latency records for your resources in multiple EC2 Regions\. When Amazon Route 53 receives a DNS query for your domain or subdomain \(example\.com or apex\.example\.com\), it determines which Amazon EC2 regions you've created latency records for, determines which region gives the user the lowest latency, and then selects a latency record for that region\. Amazon Route 53 responds with the value from the selected record, such as the IP address for a web server\. 

For example, suppose you have ELB load balancers in the US West \(Oregon\) Region and in the Asia Pacific \(Singapore\) Region\. You created a latency record for each load balancer\. Here's what happens when a user in London enters the name of your domain in a browser:

1. DNS routes the request to an Amazon Route 53 name server\.

1. Amazon Route 53 refers to its data on latency between London and the Singapore region and between London and the Oregon region\. 

1. If latency is lower between the London and Oregon regions, Amazon Route 53 responds to the query with the IP address for the Oregon load balancer\. If latency is lower between London and the Singapore region, Amazon Route 53 responds with the IP address for the Singapore load balancer Singapore\. 

Latency between hosts on the internet can change over time as a result of changes in network connectivity and routing\. Latency\-based routing is based on latency measurements performed over a period of time, and the measurements reflect these changes\. A request that is routed to the Oregon region this week might be routed to the Singapore region next week\.

**Note**  
When a browser or other viewer uses a DNS resolver that supports the edns\-client\-subnet extension of EDNS0, the DNS resolver sends Amazon Route 53 a truncated version of the user's IP address\. If you configure latency\-based routing, Amazon Route 53 considers this value when routing traffic to your resources\.

## Multivalue Answer Routing<a name="routing-policy-multivalue"></a>

Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries\. You can specify multiple values for almost any record, but multivalue answer routing also lets you check the health of each resource, so Amazon Route 53 returns only values for healthy resources\. It's not a substitute for a load balancer, but the ability to return multiple health\-checkable IP addresses is a way to use DNS to improve availability and load balancing\.

To route traffic approximately randomly to multiple resources, such as web servers, you create one multivalue answer record for each resource and, optionally, associate an Amazon Route 53 health check with each record\. Amazon Route 53 responds to DNS queries with up to eight healthy records and gives different answers to different DNS resolvers\. If a web server becomes unavailable after a resolver caches a response, client software can try another IP address in the response\.

Note the following:

+ If you associate a health check with a multivalue answer records, Amazon Route 53 responds to DNS queries with the corresponding IP address only when the health check is healthy\.

+ If you don't associate a health check with a multivalue answer record, Amazon Route 53 always considers the record to be healthy\.

+ If you have eight or fewer healthy records, Amazon Route 53 responds to all DNS queries with all the healthy records\.

+ When all records are unhealthy, Amazon Route 53 responds to DNS queries with up to eight unhealthy records\.

## Weighted Routing<a name="routing-policy-weighted"></a>

Weighted routing lets you associate multiple resources with a single domain name \(example\.com\) or subdomain name \(acme\.example\.com\) and choose how much traffic is routed to each resource\. This can be useful for a variety of purposes, including load balancing and testing new versions of software\.

To configure weighted routing, you create resource record sets that have the same name and type for each of your resources\. You assign each record a relative weight that corresponds with how much traffic you want to send to each resource\. Amazon Route 53 sends traffic to a resource based on the weight that you assign to the record as a proportion of the total weight for all records in the group: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/)

For example, if you want to send a tiny portion of your traffic to one resource and the rest to another resource, you might specify weights of 1 and 255\. The resource with a weight of 1 gets 1/256th of the traffic \(1/1\+255\), and the other resource gets 255/256ths \(255/1\+255\)\. You can gradually change the balance by changing the weights\. If you want to stop sending traffic to a resource, you can change the weight for that record to 0\.