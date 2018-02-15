# Choosing a Routing Policy<a name="routing-policy"></a>

When you create a record, you choose a routing policy, which determines how Amazon Route 53 responds to queries: 

+ **Simple routing policy** – Use for a single resource that performs a given function for your domain, for example, a web server that serves content for the example\.com website\.

+ **Failover routing policy** – Use when you want to configure active\-passive failover\. 

+ **Geolocation routing policy** – Use when you want to route traffic based on the location of your users\.

+ **Geoproximity routing policy** – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another\.

+ **Latency routing policy** – Use when you have resources in multiple locations and you want to route traffic to the resource that provides the best latency\.

+ **Multivalue answer routing policy** – Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random\.

+ **Weighted routing policy** – Use to route traffic to multiple resources in proportions that you specify\.


+ [Failover Routing](#routing-policy-failover)
+ [Geolocation Routing](#routing-policy-geo)
+ [Geoproximity Routing \(Traffic Flow Only\)](#routing-policy-geoproximity)
+ [Latency\-based Routing](#routing-policy-latency)
+ [Multivalue Answer Routing](#routing-policy-multivalue)
+ [Weighted Routing](#routing-policy-weighted)
+ [How Amazon Route 53 Estimates the Location of a User \(Geolocation and Geoproximity Routing\)](#routing-policy-edns0)

## Failover Routing<a name="routing-policy-failover"></a>

Failover routing lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy\. The primary and secondary records can route traffic to anything from an Amazon S3 bucket that is configured as a website to a complex tree of records\. For more information, see [Configuring Active\-Passive Failover by Using Amazon Route 53 Failover and Failover Alias Records](dns-failover-configuring-options.md#dns-failover-failover-rrsets) and [Configuring Failover in a Private Hosted Zone](dns-failover-private-hosted-zones.md)\. 

## Geolocation Routing<a name="routing-policy-geo"></a>

Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from\. For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region\. 

When you use geolocation routing, you can localize your content and present some or all of your website in the language of your users\. You can also use geolocation routing to restrict distribution of content to only the locations in which you have distribution rights\. Another possible use is for balancing load across endpoints in a predictable, easy\-to\-manage way, so that each user location is consistently routed to the same endpoint\. 

You can specify geographic locations by continent, by country, or by state in the United States\. If you create separate records for overlapping geographic regions—for example, one record for North America and one for Canada—priority goes to the smallest geographic region\. This allows you to route some queries for a continent to one resource and to route queries for selected countries on that continent to a different resource\. \(For a list of the countries on each continent, see [Location](resource-record-sets-values-geo.md#rrsets-values-geo-location)\.\)

Geolocation works by mapping IP addresses to locations\. However, some IP addresses aren't mapped to geographic locations, so even if you create geolocation records that cover all seven continents, Amazon Route 53 will receive some DNS queries from locations that it can't identify\. You can create a default record that handles both queries from IP addresses that aren't mapped to any location and queries that come from locations that you haven't created geolocation records for\. If you don't create a default record, Route 53 returns a "no answer" response for queries from those locations\.

For more information, see [How Amazon Route 53 Estimates the Location of a User \(Geolocation and Geoproximity Routing\)](#routing-policy-edns0)\.

## Geoproximity Routing \(Traffic Flow Only\)<a name="routing-policy-geoproximity"></a>

Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources\. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a *bias*, that expands or shrinks the size of the geographic region from which traffic is routed to a resource\.

To use geoproximity routing, you must use Route 53 [traffic flow](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/traffic-flow.html)\. You create geoproximity rules for your resources and specify one of the following values for each rule:

+ If you're using AWS resources, the AWS Region that you created the resource in

+ If you're using non\-AWS resources, the latitude and longitude of the resource

To optionally change the size of the geographic region from which Route 53 routes traffic to a resource, specify the applicable value for the bias:

+ To expand the size of the geographic region from which Route 53 routes traffic to a resource, specify a positive integer from 1 to 99 for the bias\. Route 53 shrinks the size of adjacent regions\. 

+ To shrink the size of the geographic region from which Route 53 routes traffic to a resource, specify a negative bias of \-1 to \-99\. Route 53 expands the size of adjacent regions\. 

In the following illustration, suppose you increase the bias for the record for the endpoint in Boston and decrease the bias for the record for the endpoint in Washington, D\.C\. \(You can change one value or both\.\)

+ Increasing the bias for the endpoint in Boston has the effect of increasing the geographic area that the endpoint serves\. A user in Philadelphia who was originally routed to an endpoint in Washington, D\.C\. is now routed to the endpoint in Boston\.

+ Decreasing the bias for the endpoint in Washington, D\.C\. has the effect of decreasing the geographic area that the endpoint serves\.

![\[Adding a bias, either positive or negative, can shift a user from one endpoint to another.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/geoproximity-routing-bias.png)

The effect of changing the bias for your resources depends on a number of factors, including the following:

+ The number of resources that you have\.

+ How close the resources are to one another\.

+ The number of users that you have near the border area between geographic regions\. For example, if you have resources in Boston and Washington, D\.C\. and you have a lot of users in New York City, which is roughly equidistant between your resources, a small change in bias could result in a large swing in traffic from resources in Boston to resources in D\.C\. or vice versa\.

We recommend that you change the bias in small increments to prevent overwhelming your resources due to an unanticipated swing in traffic\.

For more information, see [How Amazon Route 53 Estimates the Location of a User \(Geolocation and Geoproximity Routing\)](#routing-policy-edns0)\.

### How Amazon Route 53 Uses Bias to Route Traffic<a name="routing-policy-geoproximity-bias"></a>

Here's the formula that Amazon Route 53 uses to determine how to route traffic:

**Positive bias**  
`Biased distance = actual distance * [1 - (bias/100)]`

**Negative bias**  
`Biased distance = actual distance / [1 + (bias/100)]`

When the value of the bias is positive, Route 53 treats the source of a DNS query and the resource that you specify in a geoproximity record \(such as an EC2 instance in an AWS Region\) as if they were closer together than they really are\. For example, suppose you have the following geoproximity records:

+ A record for web server A, which has a positive bias of 50

+ A record for web server B, which has no bias

When a geoproximity record has a positive bias of 50, Route 53 halves the distance between the source of a query and the resource for that record\. Then Route 53 calculates which resource is closer to the source of the query\. Suppose web server A is 150 kilometers from the source of a query and web server B is 100 kilometers from the source of the query\. If neither record had a bias, Route 53 would route the query to web server B because it's closer\. However, because the record for web server A has a positive bias of 50, Route 53 treats web server A as if it's 75 kilometers from the source of the query\. As a result, Route 53 routes the query to web server A\. 

Here's the calculation for a positive bias of 50:

```
Bias = 50
Biased distance = actual distance * [1 - (bias/100)]

Biased distance = 150 kilometers * [1 - (50/100)]
Biased distance = 150 kilometers * (1 - .50)
Biased distance = 150 kilometers * (.50)
Biased distance = 75 kilometers
```

## Latency\-based Routing<a name="routing-policy-latency"></a>

If your application is hosted in multiple Amazon EC2 regions, you can improve performance for your users by serving their requests from the Amazon EC2 region that provides the lowest latency\. 

To use latency\-based routing, you create latency records for your resources in multiple EC2 Regions\. When Amazon Route 53 receives a DNS query for your domain or subdomain \(example\.com or apex\.example\.com\), it determines which Amazon EC2 regions you've created latency records for, determines which region gives the user the lowest latency, and then selects a latency record for that region\. Route 53 responds with the value from the selected record, such as the IP address for a web server\. 

For example, suppose you have ELB load balancers in the US West \(Oregon\) Region and in the Asia Pacific \(Singapore\) Region\. You created a latency record for each load balancer\. Here's what happens when a user in London enters the name of your domain in a browser:

1. DNS routes the request to a Route 53 name server\.

1. Route 53 refers to its data on latency between London and the Singapore region and between London and the Oregon region\. 

1. If latency is lower between the London and Oregon regions, Route 53 responds to the query with the IP address for the Oregon load balancer\. If latency is lower between London and the Singapore region, Route 53 responds with the IP address for the Singapore load balancer Singapore\. 

Latency between hosts on the internet can change over time as a result of changes in network connectivity and routing\. Latency\-based routing is based on latency measurements performed over a period of time, and the measurements reflect these changes\. A request that is routed to the Oregon region this week might be routed to the Singapore region next week\.

**Note**  
When a browser or other viewer uses a DNS resolver that supports the edns\-client\-subnet extension of EDNS0, the DNS resolver sends Route 53 a truncated version of the user's IP address\. If you configure latency\-based routing, Route 53 considers this value when routing traffic to your resources\.

## Multivalue Answer Routing<a name="routing-policy-multivalue"></a>

Multivalue answer routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries\. You can specify multiple values for almost any record, but multivalue answer routing also lets you check the health of each resource, so Route 53 returns only values for healthy resources\. It's not a substitute for a load balancer, but the ability to return multiple health\-checkable IP addresses is a way to use DNS to improve availability and load balancing\.

To route traffic approximately randomly to multiple resources, such as web servers, you create one multivalue answer record for each resource and, optionally, associate a Route 53 health check with each record\. Route 53 responds to DNS queries with up to eight healthy records and gives different answers to different DNS resolvers\. If a web server becomes unavailable after a resolver caches a response, client software can try another IP address in the response\.

Note the following:

+ If you associate a health check with a multivalue answer records, Route 53 responds to DNS queries with the corresponding IP address only when the health check is healthy\.

+ If you don't associate a health check with a multivalue answer record, Route 53 always considers the record to be healthy\.

+ If you have eight or fewer healthy records, Route 53 responds to all DNS queries with all the healthy records\.

+ When all records are unhealthy, Route 53 responds to DNS queries with up to eight unhealthy records\.

## Weighted Routing<a name="routing-policy-weighted"></a>

Weighted routing lets you associate multiple resources with a single domain name \(example\.com\) or subdomain name \(acme\.example\.com\) and choose how much traffic is routed to each resource\. This can be useful for a variety of purposes, including load balancing and testing new versions of software\.

To configure weighted routing, you create records that have the same name and type for each of your resources\. You assign each record a relative weight that corresponds with how much traffic you want to send to each resource\. Amazon Route 53 sends traffic to a resource based on the weight that you assign to the record as a proportion of the total weight for all records in the group: 

![\[Formula for how much traffic is routed to a given resource: weight for a specified record / sum of the weights for all records.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/WRR_calculation.png)

For example, if you want to send a tiny portion of your traffic to one resource and the rest to another resource, you might specify weights of 1 and 255\. The resource with a weight of 1 gets 1/256th of the traffic \(1/1\+255\), and the other resource gets 255/256ths \(255/1\+255\)\. You can gradually change the balance by changing the weights\. If you want to stop sending traffic to a resource, you can change the weight for that record to 0\.

## How Amazon Route 53 Estimates the Location of a User \(Geolocation and Geoproximity Routing\)<a name="routing-policy-edns0"></a>

To improve the accuracy of geolocation and geoproximity routing, Amazon Route 53 supports the edns\-client\-subnet extension of EDNS0\. \(EDNS0 adds several optional extensions to the DNS protocol\.\) Route 53 can use edns\-client\-subnet only when DNS resolvers support it:

+ When a browser or other viewer uses a DNS resolver that does not support edns\-client\-subnet, Route 53 uses the source IP address of the DNS resolver to approximate the location of the user and responds to geolocation queries with the DNS record for the resolver's location\.

+ When a browser or other viewer uses a DNS resolver that does support edns\-client\-subnet, the DNS resolver sends Route 53 a truncated version of the user's IP address\. Route 53 determines the location of the user based on the truncated IP address rather than the source IP address of the DNS resolver; this typically provides a more accurate estimate of the user's location\. Route 53 then responds to geolocation queries with the DNS record for the user's location\.

For more information about edns\-client\-subnet, see the IETF draft [Client Subnet in DNS Requests](https://tools.ietf.org/html/draft-ietf-dnsop-edns-client-subnet-08)\.