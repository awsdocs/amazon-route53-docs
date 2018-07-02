# Choosing Between Alias and Non\-Alias Records<a name="resource-record-sets-choosing-alias-non-alias"></a>

While ordinary Amazon Route 53 records are standard DNS records, *alias records* provide a Route 53–specific extension to DNS functionality\. Instead of an IP address or a domain name, an alias record contains a pointer to an AWS resource such as a CloudFront distribution or an Amazon S3 bucket\. When Route 53 receives a DNS query that matches the name and type in an alias record, Route 53 follows the pointer and responds with the applicable value:

+ **An alternate domain name for a CloudFront distribution** – Route 53 responds as if the query had asked for the CloudFront distribution by using the CloudFront domain name, such as d111111abcdef8\.cloudfront\.net\.

+ **An Elastic Beanstalk environment** – Route 53 responds to each query with one or more IP addresses for the environment\.

+ **An ELB load balancer** – Route 53 responds to each query with one or more IP addresses for the load balancer\. 

+ **An Amazon S3 bucket that is configured as a static website** – Route 53 responds to each query with one IP address for the Amazon S3 bucket\.

+ **Another Route 53 record in the same hosted zone** – Route 53 responds as if the query had asked for the record that is referenced by the pointer\.

If an alias record points to an AWS resource, you can't set the time to live \(TTL\); Route 53 uses the TTL for the resource\. If an alias record points to another record in the same hosted zone, Route 53 uses the TTL of the record that the alias record points to\. For more information about the current TTL value for Elastic Load Balancing, go to [Request Routing](http://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html#request-routing) in the *Elastic Load Balancing User Guide* and search for "ttl"\.

Alias records can save you time because Route 53 automatically recognizes changes in the records that the alias record refers to\. For example, suppose an alias record for example\.com points to an ELB load balancer at lb1\-1234\.us\-east\-2\.elb\.amazonaws\.com\. If the IP address of the load balancer changes, Route 53 will automatically reflect those changes in DNS answers for example\.com without any changes to the hosted zone that contains records for example\.com\.

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
| Route 53 charges for CNAME queries\. | Route 53 doesn't charge for alias queries to AWS resources\. For more information, see [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\. | 
| You can't create a CNAME record at the top node of a DNS namespace, also known as the *zone apex*\. For example, if you register the DNS name example\.com, the zone apex is example\.com\.  | You can create an alias record at the zone apex\. If you create an alias record that routes traffic to another record in the same hosted zone, and if the record that you're routing traffic to has a type of CNAME, you can't create an alias record at the zone apex\. This is because the alias record must have the same type as the record you're routing traffic to, and creating a CNAME record for the zone apex isn't supported even for an alias record\.  | 
| A CNAME record redirects queries for a domain name regardless of record type\. | Route 53 follows the pointer in an alias record only when the record type also matches\. | 
| A CNAME record can point to any DNS record that is hosted anywhere\. | An alias record can only point to one of the AWS resources listed earlier in this topic or to another record in the hosted zone that you're creating the alias record in\.  | 
| A CNAME record is visible in the answer section of a reply from a Route 53 DNS server\. | An alias record is only visible in the Route 53 console or the Route 53 API\. | 
| A CNAME record is followed by a recursive resolver\.  | An alias record is only followed inside Route 53\. This means that both the alias record and its target must exist in Route 53\. | 