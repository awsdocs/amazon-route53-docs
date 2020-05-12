# Using traffic flow to route DNS traffic<a name="traffic-flow"></a>

Managing related records in a hosted zone can be challenging in the following circumstances:
+ You have a lot of resources that perform the same operation, such as web servers that serve traffic for the same domain\.
+ You want to create a complex tree of records using [alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) and a combination of [Route 53 routing policies](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html), such as latency, failover, and weighted\. 

You can create records one at a time, but it's hard to keep track of the relationships among the records when you're reviewing the settings in the Route 53 console\. Traffic flow greatly simplifies the process of creating and maintaining records in large and complex configurations\.

**Visual editor**  
The traffic flow visual editor lets you create complex trees of records and see the relationships among the records\. For example, you might create a configuration in which latency alias records reference weighted records, and the weighted records reference your resources in multiple AWS Regions\. Each configuration is known as a *traffic policy*\. You can create as many traffic policies as you want at no charge\.

**Versioning**  
You can create multiple versions of a traffic policy so you don't have to start all over when your configuration changes\. Old versions continue to exist until you delete them; there's a default limit of 1000 versions per traffic policy\. You can optionally give each version a description\. 

**Automatic record creation and updating**  
A traffic policy can represent dozens or even hundreds of records\. Traffic flow lets you create all those records automatically by creating a *traffic policy record*\. You specify the hosted zone and the name of the record at the root of the tree, such as example\.com or www\.example\.com, and Route 53 automatically creates all the other records in the tree\. The root record—the traffic policy record—appears in the list of records for your hosted zone; all the other records are hidden\.   
When you create a new version of a traffic policy, you can selectively update traffic policy records that you created using the previous traffic policy version\. When you update a traffic policy record, Route 53 automatically updates all the other records in the tree\. You can also quickly roll back changes by updating a traffic policy record again to use a previous version of a traffic policy\.  
You can use traffic flow to create records only in public hosted zones\.

**Reuse for multiple records in different hosted zones**  
You can use a traffic policy to automatically create records in multiple public hosted zones\. For example, if you're using the same web servers for multiple domain names, you can use the same traffic policy to create traffic policy records in the hosted zones for example\.com, example\.org, and example\.net\.

**How Route 53 responds to DNS queries**  
When a client submits a query for the name of the root record, such as example\.com or www\.example\.com, Route 53 responds to the query based on the configuration in the traffic policy that you used to create the corresponding traffic policy record\.

**Geoproximity routing policy**  
The geoproximity routing policy is available only if you use traffic flow\. With geoproximity routing, you can route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another\. For more information, see [Geoproximity routing \(traffic flow only\)](routing-policy.md#routing-policy-geoproximity)\.

**Charge for traffic flow**  
There's a monthly charge for each traffic policy record\. For more information, see the "Traffic Flow" section of [Amazon Route 53 pricing](https://aws.amazon.com/route53/pricing/)\.  
To minimize these charges, you can create one or more alias records in a hosted zone that reference a traffic policy record in that hosted zone\. For example, you can create a traffic policy record for example\.com and then create an alias record for www\.example\.com that references the traffic policy record\.

**Topics**
+ [Creating and managing traffic policies](traffic-policies.md)
+ [Creating and managing policy records](traffic-policy-records.md)