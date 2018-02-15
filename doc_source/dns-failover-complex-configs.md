# How Health Checks Work in Complex Amazon Route 53 Configurations<a name="dns-failover-complex-configs"></a>

Checking the health of resources in complex configurations works much the same way as in simple configurations\. However, in complex configurations, you use a combination of alias records \(such as weighted alias and failover alias\) and nonalias records to build a decision tree that gives you greater control over how Amazon Route 53 responds to requests\. For more information, see [How Health Checks Work in Simple Amazon Route 53 Configurations](dns-failover-simple-configs.md)\.

For example, you might use latency alias records to select a region close to a user and use weighted records for two or more resources within each region to protect against the failure of a single endpoint or an Availability Zone\. The following diagram shows this configuration\.

![\[DNS configuration that includes latency alias records and weighted alias records.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-latency-alias-weighted.png)

Here's how Amazon EC2 and Route 53 are configured:

+ You have Amazon EC2 instances in two regions, us\-east\-1 and ap\-southeast\-2\. You want Route 53 to respond to queries by using the records in the region that provides the lowest latency for your customers, so you create a latency alias record for each region\. \(You create the latency alias records after you create records for the individual Amazon EC2 instances\.\)

+ Within each region, you have two Amazon EC2 instances\. You create a weighted record for each instance\. The name and the type are the same for both of the weighted records in each region\.

  When you have multiple resources in a region, you can create weighted or failover records for your resources\. You can also create even more complex configurations by creating weighted alias or failover alias records that, in turn, refer to multiple resources\.

+ Each weighted record has an associated health check\. The IP address for each health check matches the IP address for the corresponding record\. This isn't required, but it's the most common configuration\.

+ For both latency alias records, you set the value of **Evaluate Target Health** to **Yes**\.

  You use the **Evaluate Target Health** setting for each latency alias record to make Route 53 evaluate the health of the alias targets—the weighted records—and respond accordingly\.

![\[DNS configuration that includes latency alias records and weighted alias records.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-latency-alias-weighted-both-failed.png)

The preceding diagram illustrates the following sequence of events:

1. Route 53 receives a query for example\.com\. Based on the latency for the user making the request, Route 53 selects the latency alias record for the us\-east\-1 region\.

1. Route 53 selects a weighted record based on weight\. **Evaluate Target Health** is **Yes** for the latency alias record, so Route 53 checks the health of the selected weighted record\. 

1. The health check failed, so Route 53 chooses another weighted record based on weight and checks its health\. That record also is unhealthy\. 

1. Route 53 backs out of that branch of the tree, looks for the latency alias record with the next\-best latency, and chooses the record for ap\-southeast\-2\.

1. Route 53 again selects a record based on weight, and then checks the health of the selected record\. The health check passed, so Route 53 returns the applicable value in response to the query\.


+ [What Happens When You Associate a Health Check with an Alias Record?](#dns-failover-complex-configs-hc-alias)
+ [What Happens When You Omit Health Checks?](#dns-failover-complex-configs-hc-omitting)
+ [What Happens When You Set Evaluate Target Health to No?](#dns-failover-complex-configs-eth-no)

## What Happens When You Associate a Health Check with an Alias Record?<a name="dns-failover-complex-configs-hc-alias"></a>

You can associate a health check with an alias record instead of or in addition to setting the value of **Evaluate Target Health** to **Yes**\. However, it's generally more useful if Amazon Route 53 responds to queries based on the health of the underlying resources—the HTTP servers, database servers, and other resources that your alias records refer to\. For example, suppose the following configuration:

+ You assign a health check to a latency alias record for which the alias target is a group of weighted records\.

+ You set the value of **Evaluate Target Health** to **Yes** for the latency alias record\.

In this configuration, both of the following must be true before Route 53 will return the applicable value for a weighted record:

+ The health check associated with the latency alias record must pass\.

+ At least one weighted record must be considered healthy, either because it's associated with a health check that passes or because it's not associated with a health check\. In the latter case, Route 53 always considers the weighted record healthy\.

![\[DNS configuration that includes an alias record with both Evaluate Target Health set to Yes and a health check on the alias record.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-latency-alias-weighted-alias-hc-failed.png)

If the health check for the latency alias record fails, Route 53 stops responding to queries using any of the weighted records in the alias target, even if they're all healthy\. Route 53 doesn't know the status of the weighted records because it never looks past the failed health check on the alias record\.

## What Happens When You Omit Health Checks?<a name="dns-failover-complex-configs-hc-omitting"></a>

In a complex configuration, it's important to associate health checks with all of the non\-alias records\. Let's return to the preceding example, but assume that a health check is missing on one of the weighted records in the us\-east\-1 region:

![\[DNS configuration that includes one failed health check and one record that has no health check.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-latency-alias-weighted-missing-health-check.png)

Here's what happens when you omit a health check on a non\-alias record in this configuration:

1. Route 53 receives a query for example\.com\. Based on the latency for the user making the request, Route 53 selects the latency alias record for the us\-east\-1 region\.

1. Route 53 looks up the alias target for the latency alias record, and checks the status of the corresponding health checks\. The health check for one weighted record failed, so that record is omitted from consideration\.

1. The other weighted record in the alias target for the us\-east\-1 region has no health check\. The corresponding resource might or might not be healthy, but without a health check, Route 53 has no way to know\. Route 53 assumes that the resource is healthy and returns the applicable value in response to the query\.

## What Happens When You Set Evaluate Target Health to No?<a name="dns-failover-complex-configs-eth-no"></a>

In general, you also want to set **Evaluate Target Health** to **Yes** for all of the alias records\. In the following example, all of the weighted records have associated health checks, but **Evaluate Target Health** is set to **No** for the latency alias record for the us\-east\-1 region:

![\[DNS configuration that includes an alias record with Evaluate Target Health set to No.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/hc-latency-alias-weighted-eth-is-no.png)

Here's what happens when you set **Evaluate Target Health** to **No** for an alias record in this configuration:

1. Amazon Route 53 receives a query for example\.com\. Based on the latency for the user making the request, Route 53 selects the latency alias record for the us\-east\-1 region\.

1. Route 53 determines what the alias target is for the latency alias record, and checks the corresponding health checks\. They're both failing\.

1. Because the value of **Evaluate Target Health** is **No** for the latency alias record for the us\-east\-1 region, Route 53 must choose one record in this branch instead of backing out of the branch and looking for a healthy record in the ap\-southeast\-2 region\.