# How Amazon Route 53 averts failover problems<a name="dns-failover-problems"></a>

The failover algorithms implemented by Route 53 are designed not only to route traffic to endpoints that are healthy, but also to avoid making disaster scenarios worse due to misconfigured health checks and applications, endpoint overloads, and partition failures\.

**Topics**
+ [How Amazon Route 53 averts cascading failures](#dns-failover-cascading-failures)
+ [How Amazon Route 53 handles internet partitions](#dns-failover-internet-partitions)

## How Amazon Route 53 averts cascading failures<a name="dns-failover-cascading-failures"></a>

As a first defense against cascading failures, each request routing algorithm \(such as weighted and failover\) has a mode of last resort\. In this special mode, when all records are considered unhealthy, the Route 53 algorithm reverts to considering all records healthy\.

For example, if all instances of an application, on several hosts, are rejecting health check requests, Route 53 DNS servers will choose an answer anyway and return it rather than returning no DNS answer or returning an NXDOMAIN \(non\-existent domain\) response\. An application can respond to users but still fail health checks, so this provides some protection against misconfiguration\.

Similarly, if an application is overloaded, and one out of three endpoints fails its health checks, so that it's excluded from Route 53 DNS responses, Route 53 distributes responses between the two remaining endpoints\. If the remaining endpoints are unable to handle the additional load and they fail, Route 53 reverts to distributing requests to all three endpoints\.

## How Amazon Route 53 handles internet partitions<a name="dns-failover-internet-partitions"></a>

Although uncommon, there occasionally are significant internet partitions, meaning that large geographic regions can't communicate with one another over the internet\. During these partitions, Route 53 locations might reach different conclusions about the health status of an endpoint and might differ from the status reported to CloudWatch\. Route 53 health checkers in each AWS Region are constantly sending health check statuses to all Route 53 locations\. During internet partitions, each Route 53 location might have access only to a partial set of these statuses, usually from its closest regions\.

For example, during an internet partition that affects connectivity to and from South America, the Route 53 DNS servers in the Route 53 South America \(São Paulo\) location might have good access to the health check endpoints in the South America \(São Paulo\) AWS Region, but poor access to endpoints elsewhere\. At the same time, Route 53 in US East \(Ohio\) might have poor access to health check endpoints in the South America \(São Paulo\) Region, and conclude that the corresponding records are unhealthy\.

Partitions such as these can give rise to situations where Route 53 locations make different conclusions about the health status of endpoints, based on their local visibility of those endpoints\. This is why each Route 53 location considers an endpoint healthy when only a portion of reachable health checkers consider it healthy\.