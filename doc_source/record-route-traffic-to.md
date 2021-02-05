# Value/route traffic to<a name="record-route-traffic-to"></a>

For **Value/route traffic to**, choose the applicable value:
+ **To route traffic to an AWS resource that appears in the list**: choose the type of the resource, such as a CloudFront distribution or an Amazon S3 website endpoint\. Then specify the applicable values, such as the AWS Region where you created the resource, and the resource that you want to route traffic to\.
+ **To route traffic to a type of AWS resource that isn't listed**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
+ **To create other types of records, such as TXT records**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.

Choose **Alias** if you want to route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets, or if you want to route traffic from one record in a hosted zone to another record\. 

If your alias record points to an AWS resource or another record in the same hosted zone, you can't set the time to live \(TTL\)\. This is because Route 53 uses the default TTL for the resource or the record that the alias record points to\. 

## Learn more<a name="record-route-traffic-to-learn-more"></a>
+ [Working with records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)
+ [Choosing between alias and non\-alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias)
+ [Values for alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-values-alias.html)