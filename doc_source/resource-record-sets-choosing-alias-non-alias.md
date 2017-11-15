# Choosing Between Alias and Non\-Alias Resource Record Sets<a name="resource-record-sets-choosing-alias-non-alias"></a>

While ordinary Amazon Route 53 resource record sets are standard DNS resource record sets, *alias resource record sets* provide an Amazon Route 53–specific extension to DNS functionality\. Instead of an IP address or a domain name, an alias resource record set contains a pointer to a CloudFront distribution, an Elastic Beanstalk environment, an ELB Classic, Application, or Network Load Balancer, an Amazon S3 bucket that is configured as a static website, or another Amazon Route 53 resource record set in the same hosted zone\. When Amazon Route 53 receives a DNS query that matches the name and type in an alias resource record set, Amazon Route 53 follows the pointer and responds with the applicable value:

+ **An alternate domain name for a CloudFront distribution** – Amazon Route 53 responds as if the query had asked for the CloudFront distribution by using the CloudFront domain name, such as d111111abcdef8\.cloudfront\.net\.
**Note**  
You can't create alias resource record sets for CloudFront distributions in a private hosted zone\.

+ **An Elastic Beanstalk environment** – Amazon Route 53 responds to each request with one or more IP addresses for the environment\.

+ **An ELB load balancer** – Amazon Route 53 responds to each request with one or more IP addresses for the load balancer\. 

+ **An Amazon S3 bucket that is configured as a static website** – Amazon Route 53 responds to each request with one IP address for the Amazon S3 bucket\.

+ **Another Amazon Route 53 resource record set in the same hosted zone** – Amazon Route 53 responds as if the query had asked for the resource record set that is referenced by the pointer\.

If an alias resource record set points to a CloudFront distribution, an Elastic Beanstalk environment, an ELB load balancer, or an Amazon S3 bucket, you cannot set the time to live \(TTL\); Amazon Route 53 uses the CloudFront, Elastic Beanstalk, Elastic Load Balancing, or Amazon S3 TTLs\. If an alias resource record set points to another resource record set in the same hosted zone, Amazon Route 53 uses the TTL of the resource record set that the alias resource record set points to\. For more information about the current TTL value for Elastic Load Balancing, go to [Request Routing](http://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html#request-routing) in the *Elastic Load Balancing User Guide* and search for "ttl"\.

Alias resource record sets can save you time because Amazon Route 53 automatically recognizes changes in the resource record sets that the alias resource record set refers to\. For example, suppose an alias resource record set for example\.com points to an ELB load balancer at lb1\-1234\.us\-east\-2\.elb\.amazonaws\.com\. If the IP address of the load balancer changes, Amazon Route 53 will automatically reflect those changes in DNS answers for example\.com without any changes to the hosted zone that contains resource record sets for example\.com\.

For information about creating resource record sets by using the Amazon Route 53 console, see [Creating Resource Record Sets by Using the Amazon Route 53 Console](resource-record-sets-creating.md)\. For information about the values that you specify for alias resource record sets, see the applicable topic in [Values That You Specify When You Create or Edit Amazon Route 53 Records](resource-record-sets-values.md):

+ [Values for Alias Resource Record Sets](resource-record-sets-values-alias.md)

+ [Values for Weighted Alias Resource Record Sets](resource-record-sets-values-weighted-alias.md)

+ [Values for Latency Alias Resource Record Sets](resource-record-sets-values-latency-alias.md)

+ [Values for Failover Alias Resource Record Sets](resource-record-sets-values-failover-alias.md)

+ [Values for Geolocation Alias Resource Record Sets](resource-record-sets-values-geo-alias.md)

Alias resource records sets are similar to CNAME records, but there are some important differences:


****  

| CNAME Records | Alias Records | 
| --- | --- | 
| Amazon Route 53 charges for CNAME queries\. | Amazon Route 53 doesn't charge for alias queries to CloudFront distributions, Elastic Beanstalk environments, ELB load balancers, or Amazon S3 buckets\. For more information, see [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\. | 
| You can't create a CNAME record at the top node of a DNS namespace, also known as the *zone apex*\. For example, if you register the DNS name example\.com, the zone apex is example\.com\.  | You can create an alias resource record set at the zone apex\. If you create an alias record that routes traffic to another record in the same hosted zone, and if the record that you're routing traffic to has a type of CNAME, you can't create an alias record at the zone apex\. This is because the alias record must have the same type as the record you're routing traffic to, and creating a CNAME record for the zone apex isn't supported even for an alias record\.  | 
| A CNAME record redirects queries for a domain name regardless of record type\. | Amazon Route 53 follows the pointer in an alias resource record set only when the record type also matches\. | 
| A CNAME record can point to any DNS record hosted anywhere, including to the resource record set that Amazon Route 53 automatically creates when you create a policy record\. For more information, see [Using Traffic Flow to Route DNS Traffic](traffic-flow.md)\. | An alias resource record set can only point to a CloudFront distribution, an Elastic Beanstalk environment, an ELB load balancer, an Amazon S3 bucket that is configured as a static website, or another resource record set in the same Amazon Route 53 hosted zone in which you're creating the alias resource record set\. However, you can't create an alias that points to the resource record set that Amazon Route 53 creates when you create a policy record\. | 
| A CNAME record is visible in the answer section of a reply from an Amazon Route 53 DNS server\. | An alias resource record set is only visible in the Amazon Route 53 console or the Amazon Route 53 API\. | 
| A CNAME record is followed by a recursive resolver\.  | An alias resource record set is only followed inside Amazon Route 53\. This means that both the alias resource record set and its target must exist in Amazon Route 53\. | 