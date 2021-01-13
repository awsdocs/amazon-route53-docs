# Alias<a name="record-alias"></a>

Choose this option if you want to route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets, or if you want to route traffic from one record in a hosted zone to another record\. 

If your alias record points to an AWS resource or another record in the same hosted zone, you can't set the time to live \(TTL\)\. This is because Route 53 uses the default TTL for the resource or the record that the alias record points to\. 

## Learn more<a name="record-type-learn-more"></a>
+ [Choosing between alias and non\-alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias)
+ [Values for alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-values-alias.html)