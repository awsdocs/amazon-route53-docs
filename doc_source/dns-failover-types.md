# Active\-active and active\-passive failover<a name="dns-failover-types"></a>

You can use Route 53 health checking to configure active\-active and active\-passive failover configurations\. You configure active\-active failover using any [routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html) \(or combination of routing policies\) other than failover, and you configure active\-passive failover using the failover routing policy\.

**Topics**
+ [Active\-active failover](#dns-failover-types-active-active)
+ [Active\-passive failover](#dns-failover-types-active-passive)

## Active\-active failover<a name="dns-failover-types-active-active"></a>

Use this failover configuration when you want all of your resources to be available the majority of the time\. When a resource becomes unavailable, Route 53 can detect that it's unhealthy and stop including it when responding to queries\.

In active\-active failover, all the records that have the same name, the same type \(such as A or AAAA\), and the same routing policy \(such as weighted or latency\) are active unless Route 53 considers them unhealthy\. Route 53 can respond to a DNS query using any healthy record\.

## Active\-passive failover<a name="dns-failover-types-active-passive"></a>

Use an active\-passive failover configuration when you want a primary resource or group of resources to be available the majority of the time and you want a secondary resource or group of resources to be on standby in case all the primary resources become unavailable\. When responding to queries, Route 53 includes only the healthy primary resources\. If all the primary resources are unhealthy, Route 53 begins to include only the healthy secondary resources in response to DNS queries\.

**Topics**
+ [Configuring active\-passive failover with one primary and one secondary resource](#dns-failover-types-active-passive-one-resource)
+ [Configuring active\-passive failover with multiple primary and secondary resources](#dns-failover-types-active-passive-multiple-resources)
+ [Configuring active\-passive failover with weighted records](#dns-failover-types-active-passive-weighted)

### Configuring active\-passive failover with one primary and one secondary resource<a name="dns-failover-types-active-passive-one-resource"></a>

To create an active\-passive failover configuration with one primary record and one secondary record, you just create the records and specify **Failover** for the routing policy\. When the primary resource is healthy, Route 53 responds to DNS queries using the primary record\. When the primary resource is unhealthy, Route 53 responds to DNS queries using the secondary record\.

### Configuring active\-passive failover with multiple primary and secondary resources<a name="dns-failover-types-active-passive-multiple-resources"></a>

You can also associate multiple resources with the primary record, the secondary record, or both\. In this configuration, Route 53 considers the primary failover record to be healthy as long as at least one of the associated resources is healthy\. For more information, see [How Amazon Route 53 chooses records when health checking is configuredHow Route 53 chooses records when health checking is configured](health-checks-how-route-53-chooses-records.md)\.

To configure active\-passive failover with multiple resources for the primary or secondary record, perform the following tasks\.

1. Create a health check for each resource that you want to route traffic to, such as an EC2 instance or a web server in your data center\.
**Note**  
If you're routing traffic to any AWS resources that you can create [alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) for, don't create health checks for those resources\. When you create the alias records, you set **Evaluate Target Health** to **Yes** instead\.

   For more information, see [Creating and updating health checks](health-checks-creating.md)\.

1. Create records for your primary resources, and specify the following values:
   + Give each record the same name, type, and routing policy\. For example, you might create three weighted A records that are all named failover\-primary\.example\.com\.
   + If you're using AWS resources that you can create alias records for, specify **Yes** for **Evaluate Target Health\.**

     If you're using resources that you can't create alias records for, associate the applicable health check from step 1 with each record\.

   For more information, see [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)\.

1. Create records for your secondary resources, if applicable, and specify the following values:
   + Give each record the same name, type, and routing policy\. For example, you might create three weighted A records that are all named failover\-secondary\.example\.com\.
   + If you're using AWS resources that you can create alias records for, specify **Yes** for **Evaluate Target Health\.**

     If you're using resources that you can't create alias records for, associate the applicable health check from step 1 with each record\.
**Note**  
Some customers use a web server as their primary resource and an Amazon S3 bucket that is configured as a website endpoint as their secondary resource\. The S3 bucket contains a simple "temporarily unavailable" message\. If you're using that configuration, you can skip this step and just create a failover alias record for the secondary resource in step 4\.

1. Create two failover alias records, one primary and one secondary, and specify the following values:  
**Primary record**  
   + **Name** – Specify the domain name \(example\.com\) or the subdomain name \(www\.example\.com\) that you want Route 53 to route traffic for\.
   + **Alias** – Specify **Yes**\.
   + **Alias Target** – Specify the name of the records that you created in step 2\.
   + **Routing Policy** – Specify **Failover**\.
   + **Failover Record Type** – Specify **Primary**\.
   + **Evaluate Target Health** – Specify **Yes**\.
   + **Associate with Health Check** – Specify **No**\.  
**Secondary record**  
   + **Name** – Specify the same name that you specified for the primary record\.
   + **Alias** – Specify **Yes**\.
   + **Alias Target** – If you created records for your secondary resource in step 3, specify the name of the records\. If you're using an Amazon S3 bucket for the secondary resource, specify the DNS name of the website endpoint\.
   + **Routing Policy** – Specify **Failover**\.
   + **Failover Record Type** – Specify **Secondary**\.
   + **Evaluate Target Health** – Specify **Yes**\.
   + **Associate with Health Check** – Specify **No**\.

### Configuring active\-passive failover with weighted records<a name="dns-failover-types-active-passive-weighted"></a>

You can also use weighted records for active\-passive failover, with caveats\. If you specify nonzero weights for some records and zero weights for other records, Route 53 responds to DNS queries using only healthy records that have nonzero weights\. If all the records that have a weight greater than 0 are unhealthy, then Route 53 responds to queries using the zero\-weighted records\.

**Note**  
All the records with nonzero weights must be unhealthy before Route 53 starts to respond to DNS queries using records that have weights of zero\. This can make your web application or website unreliable if the last healthy resource, such as a web server, can't handle all the traffic when other resources are unavailable\.