# Values specific for weighted alias records<a name="resource-record-sets-values-weighted-alias"></a>

When you create weighted alias records, you specify the following values\. For more information, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**Topics**
+ [Routing policy](#rrsets-values-weighted-alias-routing-policy)
+ [Record name](#rrsets-values-weighted-alias-name)
+ [Record type](#rrsets-values-weighted-alias-type)
+ [Value/Route traffic to](#rrsets-values-weighted-alias-alias-target)
+ [Weight](#rrsets-values-weighted-alias-weight)
+ [Health check](#rrsets-values-weighted-alias-associate-with-health-check)
+ [Evaluate target health](#rrsets-values-weighted-alias-evaluate-target-health)
+ [Record ID](#rrsets-values-weighted-alias-set-identifier)

## Routing policy<a name="rrsets-values-weighted-alias-routing-policy"></a>

Choose **Weighted**\.

## Record name<a name="rrsets-values-weighted-alias-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

Enter the same name for all of the records in the group of weighted records\. 

For more information about record names, see [Record name](resource-record-sets-values-alias-common.md#rrsets-values-common-alias-name)

## Record type<a name="rrsets-values-weighted-alias-type"></a>

The DNS record type\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

Select the applicable value based on the AWS resource that you're routing traffic to:

**API Gateway custom regional API or edge\-optimized API**  
Select **A — IPv4 address**\.

**Amazon VPC interface endpoints**  
Select **A — IPv4 address**\.

**CloudFront distribution**  
Select **A — IPv4 address**\.  
If IPv6 is enabled for the distribution, create two records, one with a value of **A — IPv4 address** for **Record type**, and one with a value of **AAAA — IPv6 address**\.

**Elastic Beanstalk environment that has regionalized subdomains**  
Select **A — IPv4 address**

**ELB load balancer**  
Select **A — IPv4 address** or **AAAA — IPv6 address**

**Amazon S3 bucket**  
Select **A — IPv4 address**

**Another record in this hosted zone**  
Select the type of the record that you're creating the alias for\. All types are supported except **NS** and **SOA**\.  
If you're creating an alias record that has the same name as the hosted zone \(known as the *zone apex*\), you can't route traffic to a record for which the value of **Record type** is **CNAME**\. This is because the alias record must have the same type as the record you're routing traffic to, and creating a CNAME record for the zone apex isn't supported even for an alias record\. 

Select the same value for all of the records in the group of weighted records\.

## Value/Route traffic to<a name="rrsets-values-weighted-alias-alias-target"></a>

The value that you choose from the list or that you type in the field depends on the AWS resource that you're routing traffic to\.

For information about what AWS resources you can target, see [common values for alias records for value/route traffic to](resource-record-sets-values-alias-common.md#rrsets-values-alias-common-target)\.

For more information about how to configure Route 53 to route traffic to specific AWS resources, see [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.

## Weight<a name="rrsets-values-weighted-alias-weight"></a>

A value that determines the proportion of DNS queries that Route 53 responds to using the current record\. Route 53 calculates the sum of the weights for the records that have the same combination of DNS name and type\. Route 53 then responds to queries based on the ratio of a resource's weight to the total\. 

You can't create non\-weighted records that have the same values for **Record name** and **Record type** as weighted records\.

Enter an integer between 0 and 255\. To disable routing to a resource, set **Weight** to 0\. If you set **Weight** to 0 for all of the records in the group, traffic is routed to all resources with equal probability\. This ensures that you don't accidentally disable routing for a group of weighted records\.

The effect of setting **Weight** to 0 is different when you associate health checks with weighted records\. For more information, see [How Amazon Route 53 chooses records when health checking is configuredHow Route 53 chooses records when health checking is configured](health-checks-how-route-53-chooses-records.md)\.

## Health check<a name="rrsets-values-weighted-alias-associate-with-health-check"></a>

Select a health check if you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy\. 

Route 53 doesn't check the health of the endpoint specified in the record, for example, the endpoint specified by the IP address in the **Value** field\. When you select a health check for a record, Route 53 checks the health of the endpoint that you specified in the health check\. For information about how Route 53 determines whether an endpoint is healthy, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

Associating a health check with a record is useful only when Route 53 is choosing between two or more records to respond to a DNS query, and you want Route 53 to base the choice in part on the status of a health check\. Use health checks only in the following configurations:
+ You're checking the health of all of the records in a group of records that have the same name, type, and routing policy \(such as failover or weighted records\), and you specify health check IDs for all the records\. If the health check for a record specifies an endpoint that is not healthy, Route 53 stops responding to queries using the value for that record\.
+ You select **Yes** for **Evaluate target health** for an alias record or the records in a group of failover alias, geolocation alias, latency alias, or weighted alias record\. If the alias records reference non\-alias records in the same hosted zone, you must also specify health checks for the referenced records\. If you associate a health check with an alias record and also select **Yes** for **Evaluate Target Health**, both must evaluate to true\. For more information, see [What happens when you associate a health check with an alias record?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-alias)\.

If your health checks specify the endpoint only by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the records \(example\.com\)\.

**Important**  
In this configuration, if you create a health check for which the value of **Domain name** matches the name of the records and then associate the health check with those records, health check results will be unpredictable\.

## Evaluate target health<a name="rrsets-values-weighted-alias-evaluate-target-health"></a>

Select **Yes** if you want Route 53 to determine whether to respond to DNS queries using this record by checking the health of the resource specified by **Endpoint**\. 

Note the following:

**API Gateway custom regional APIs and edge\-optimized APIs**  
There are no special requirements for setting **Evaluate target health** to **Yes** when the endpoint is an API Gateway custom Regional API or an edge\-optimized API\.

**CloudFront distributions**  
You can't set **Evaluate target health** to **Yes** when the endpoint is a CloudFront distribution\.

**Elastic Beanstalk environments that have regionalized subdomains**  
If you specify an Elastic Beanstalk environment in **Endpoint** and the environment contains an ELB load balancer, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. \(An environment automatically contains an ELB load balancer if it includes more than one Amazon EC2 instance\.\) If you set **Evaluate target health** to **Yes** and either no Amazon EC2 instances are healthy or the load balancer itself is unhealthy, Route 53 routes queries to other available resources that are healthy, if any\.   
If the environment contains a single Amazon EC2 instance, there are no special requirements\.

**ELB load balancers**  
Health checking behavior depends on the type of load balancer:  
+ **Classic Load Balancers** – If you specify an ELB Classic Load Balancer in **Endpoint**, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. If you set **Evaluate Target Health** to **Yes** and either no EC2 instances are healthy or the load balancer itself is unhealthy, Route 53 routes queries to other resources\.
+ **Application and Network Load Balancers** – If you specify an ELB Application or Network Load Balancer and you set **Evaluate Target Health** to **Yes**, Route 53 routes queries to the load balancer based on the health of the target groups that are associated with the load balancer:
  + For an Application or Network Load Balancer to be considered healthy, every target group that contains targets must contain at least one healthy target\. If any target group contains only unhealthy targets, the load balancer is considered unhealthy, and Route 53 routes queries to other resources\.
  + A target group that has no registered targets is considered unhealthy\.
When you create a load balancer, you configure settings for Elastic Load Balancing health checks; they're not Route 53 health checks, but they perform a similar function\. Do not create Route 53 health checks for the EC2 instances that you register with an ELB load balancer\. 

**S3 buckets**  
There are no special requirements for setting **Evaluate target health** to **Yes** when the endpoint is an S3 bucket\.

**Amazon VPC interface endpoints**  
There are no special requirements for setting **Evaluate target health** to **Yes** when the endpoint is an Amazon VPC interface endpoint\.

**Other records in the same hosted zone**  
If the AWS resource that you specify in **Endpoint** is a record or a group of records \(for example, a group of weighted records\) but is not another alias record, we recommend that you associate a health check with all of the records in the endpoint\. For more information, see [What happens when you omit health checks?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-omitting)\.

## Record ID<a name="rrsets-values-weighted-alias-set-identifier"></a>

Enter a value that uniquely identifies this record in the group of weighted records\.