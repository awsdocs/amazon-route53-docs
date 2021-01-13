# Weight<a name="record-weighted-weight"></a>

A value that determines the proportion of DNS queries that Route 53 responds to using the current record\. Route 53 calculates the sum of the weights for the records that have the same combination of DNS name and type\. Route 53 then responds to queries based on the ratio of a resource's weight to the total\.

To disable routing to a resource, set Weight to 0\. If you set Weight to 0 for all of the records in the group, traffic is routed to all resources with equal probability\. This ensures that you don't accidentally disable routing for a group of weighted records\.

The effect of setting Weight to 0 is different when you associate health checks with weighted records\. For more information, see [How Amazon Route 53 chooses records when health checking is configured](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-how-route-53-chooses-records.html)\.

## Learn more<a name="record-weighted-weight-learn-more"></a>
+ [Working with records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)