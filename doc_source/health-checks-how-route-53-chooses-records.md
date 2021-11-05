# How Amazon Route 53 chooses records when health checking is configured<a name="health-checks-how-route-53-chooses-records"></a>

If you configure health checking for all the records in a group of records that have the same name, the same type \(such as A or AAAA\), and the same routing policy \(such as weighted or failover\), Route 53 responds to DNS queries by choosing a healthy record and returning the applicable value from that record\.

For example, suppose you create three weighted A records, and you assign health checks to all three\. If the health check for one of the records is unhealthy, Route 53 responds to DNS queries with the IP addresses in one of the other two records\.

Here's how Route 53 chooses a healthy record:

1. Route 53 initially chooses a record based on the routing policy and on the values that you specify for each record\. For example, for weighted records, Route 53 chooses a record based on the weight that you specify for each record\.

1. Route 53 determines whether the record is healthy:
   + **Non\-alias record with an associated health check** – If you associated a health check with a non\-alias record, Route 53 checks the current status of the health check\. 

     Route 53 periodically checks the health of the endpoint that is specified in a health check; it doesn't perform the health check when the DNS query arrives\.

     You can associate health checks with alias records, but we recommend that you associate health checks only with non\-alias records\. For more information, see [What happens when you associate a health check with an alias record?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-alias)\.
   + **Alias record with Evaluate Target Health set to Yes** – Route 53 checks the health status of the resource that the alias record references, for example, an ELB load balancer or another record in the same hosted zone\.

1. If the record is healthy, Route 53 responds to the query with the applicable value, such as an IP address\.

   If the record is unhealthy, Route 53 chooses another record using the same criteria and repeats the process until it finds a healthy record\.

Route 53 uses the following criteria when choosing a record:

**Records without a health check are always healthy**  
If a record in a group of records that have the same name and type doesn't have an associated health check, Route 53 always considers it healthy and always includes it among possible responses to a query\.

**If no record is healthy, all records are healthy**  
If none of the records in a group of records are healthy, Route 53 needs to return something in response to DNS queries, but it has no basis for choosing one record over another\. In this circumstance, Route 53 considers all the records in the group to be healthy and selects one based on the routing policy and on the values that you specify for each record\.

**Weighted records that have a weight of 0**  
If you add health checks to all the records in a group of weighted records, but you give nonzero weights to some records and zero weights to others, health checks work the same as when all records have nonzero weights with the following exceptions:  
+ Route 53 initially considers only the nonzero weighted records, if any\.
+ If all the records that have a weight greater than 0 are unhealthy, then Route 53 considers the zero\-weighted records\.
For more information about weighted records, see [Weighted routing](routing-policy.md#routing-policy-weighted)\.

**Alias records**  
You can also configure health checking for alias records by setting **Evaluate Target Health** to **Yes** for each alias record\. This causes Route 53 to evaluate the health of the resource that the record routes traffic to, for example, an ELB load balancer or another record in the same hosted zone\.  
For example, suppose the alias target for an alias record is a group of weighted records that all have nonzero weights:  
+ As long as at least one of the weighted records is healthy, Route 53 considers the alias record to be healthy\.
+ If none of the weighted records is healthy, Route 53 considers the alias record to be unhealthy\.
+ Route 53 stops considering records in that branch of the tree until at least one weighted record becomes healthy again\.
For more information, see [How health checks work in complex Amazon Route 53 configurationsHow health checks work in complex configurations](dns-failover-complex-configs.md)\.

**Failover records**  
Failover records generally work the same way as other routing types\. You create health checks and associate them with non\-alias records, and you set **Evaluate Target Health** to **Yes** for alias records\. Note the following:  
+ Both the primary and secondary records can be a non\-alias record or an alias record\.
+ If you associate health checks with both the primary and secondary failover records, here's how Route 53 responds to requests:
  + If Route 53 considers the primary record healthy \(if the health check endpoint is healthy\), Route 53 returns only the primary record in response to a DNS query\.
  + If Route 53 considers the primary record unhealthy and the secondary record healthy, Route 53 returns the secondary record instead\.
  + If Route 53 considers both the primary and secondary records unhealthy, Route 53 returns the primary record\.
+ When you're configuring the secondary record, adding a health check is optional\. If you omit the health check for the secondary record, and if the health check endpoint for the primary record is unhealthy, Route 53 always responds to DNS queries by using the secondary record\. This is true even if the secondary record is unhealthy\.
For more information, see the following topics:  
+ [Configuring active\-passive failover with one primary and one secondary resource](dns-failover-types.md#dns-failover-types-active-passive-one-resource)
+ [Configuring active\-passive failover with multiple primary and secondary resources](dns-failover-types.md#dns-failover-types-active-passive-multiple-resources)