# Choosing Between Alias and Non\-Alias Records<a name="resource-record-sets-choosing-alias-non-alias"></a>

Amazon Route 53 *alias records* provide a Route 53–specific extension to DNS functionality\. Alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets\. They also let you route traffic from one record in a hosted zone to another record\. 

Unlike a CNAME record, you can create an alias record at the top node of a DNS namespace, also known as the *zone apex*\. For example, if you register the DNS name example\.com, the zone apex is example\.com\. You can't create a CNAME record for example\.com, but you can create an alias record for example\.com that routes traffic to www\.example\.com\.

When Route 53 receives a DNS query for an alias record, Route 53 responds with the applicable value for that resource:
+ **An Amazon API Gateway custom regional API or edge\-optimized API** – Route 53 responds with one or more IP addresses for your API\.
+ **An Amazon VPC interface endpoint** – Route 53 responds with one or more IP addresses for your interface endpoint\.
+ **A CloudFront distribution** – Route 53 responds with one or more IP addresses for CloudFront edge servers that can serve your content\.
+ **An Elastic Beanstalk environment** – Route 53 responds with one or more IP addresses for the environment\.
+ **An ELB load balancer** – Route 53 responds with one or more IP addresses for the load balancer\. 
+ **An Amazon S3 bucket that is configured as a static website** – Route 53 responds with one IP address for the Amazon S3 bucket\.
+ **Another Route 53 record in the same hosted zone** – Route 53 responds as if the query is for the record that is referenced by the alias record\.

When you use an alias record to route traffic to an AWS resource, Route 53 automatically recognizes changes in the resource\. For example, suppose an alias record for example\.com points to an ELB load balancer at lb1\-1234\.us\-east\-2\.elb\.amazonaws\.com\. If the IP address of the load balancer changes, Route 53 automatically starts to respond to DNS queries using the new IP address\.

If an alias record points to an AWS resource, you can't set the time to live \(TTL\); Route 53 uses the default TTL for the resource\. If an alias record points to another record in the same hosted zone, Route 53 uses the TTL of the record that the alias record points to\. For more information about the current TTL value for Elastic Load Balancing, go to [Request Routing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html#request-routing) in the *Elastic Load Balancing User Guide* and search for "ttl"\.

For information about creating records by using the Route 53 console, see [Creating Records by Using the Amazon Route 53 Console](resource-record-sets-creating.md)\. For information about the values that you specify for alias records, see the applicable topic in [Values That You Specify When You Create or Edit Amazon Route 53 Records](resource-record-sets-values.md):
+ [Values for Alias Records](resource-record-sets-values-alias.md)
+ [Values for Weighted Alias Records](resource-record-sets-values-weighted-alias.md)
+ [Values for Latency Alias Records](resource-record-sets-values-latency-alias.md)
+ [Values for Failover Alias Records](resource-record-sets-values-failover-alias.md)
+ [Values for Geolocation Alias Records](resource-record-sets-values-geo-alias.md)

Alias records are similar to CNAME records, but there are some important differences:


****  

| CNAME Records | Alias Records | 
| --- | --- | 
| A CNAME record can redirect DNS queries to any DNS record\. For example, you can create a CNAME record that redirects queries from acme\.example\.com to zenith\.example\.com or to acme\.example\.org\. You don't need to use Route 53 as the DNS service for the domain that you're redirecting queries to\. | An alias record can only redirect queries to selected AWS resources, such as the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) For example, you can create an alias record named acme\.example\.com that redirects queries to an Amazon S3 bucket that is also named acme\.example\.com\. You can also create an acme\.example\.com alias record that redirects queries to a record named zenith\.example\.com in the example\.com hosted zone\. | 
| You can't create a CNAME record at the zone apex\. For example, if you register the DNS name example\.com, the zone apex is example\.com\.  | In most configurations, you can create an alias record at the zone apex\. The one exception is when you want to redirect queries from the zone apex \(such as example\.com\) to a record in the same hosted zone that has a type of CNAME \(such as acme\.example\.com\)\. The alias record must have the same type as the record you're routing traffic to, and creating a CNAME record for the zone apex isn't supported even for an alias record\.  | 
| Route 53 charges for CNAME queries\. | Route 53 doesn't charge for alias queries to AWS resources\. For more information, see [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\. | 
| A CNAME record redirects DNS queries for a record name regardless of record type, such as A or AAAA\. | Route 53 responds to a DNS query only when the name of the alias record \(such as acme\.example\.com\) and the type of the alias record \(such as A or AAAA\) match the name and type in the DNS query\. | 
| A CNAME record appears as a CNAME record in response to dig or nslookup queries\. | An alias record appears as the record type that you specified when you created the record, such as A or AAAA\. The alias property is visible only in the Route 53 console or in the response to a programmatic request, such as an AWS CLI `list-resource-record-sets` command\. | 