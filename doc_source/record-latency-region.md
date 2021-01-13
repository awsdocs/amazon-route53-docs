# Region \(latency records\)<a name="record-latency-region"></a>

The Amazon EC2 Region where the resource that you specified in this record resides\. Route 53 recommends an Amazon EC2 Region based on other values that you've specified\. We recommend that you not change this value\.

Note the following:
+ You can only create one latency record for each Amazon EC2 Region\.
+ You aren't required to create latency records for all Amazon EC2 Regions\. Route 53 chooses the Region with the best latency from among the Regions that you create latency records for\.
+ If you create a record tagged with the Region **cn\-north\-1**, Route 53 always responds to queries from within China using this record, regardless of the latency\.

## Learn more<a name="record-latency-region-learn-more"></a>
+ [Working with records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)