# Weighted records to add to *domain\-name*<a name="routing-weighted"></a>

Each weighted record that you define has the same name, type, and TTL that you specified in the **Basic configuration**\. In addition, each record has the following values:
+ **Record ID**: When you create records that have a routing policy other than simple, enter a value that uniquely identifies each record that has the same name and type\. For example, you might assign a date/time stamp or a sequential counter\. 
+ **Weight**: The value of **Weight** determines the proportion of DNS queries that Route 53 responds to using the current record\. Route 53 adds the weights for the records that have the same DNS name and type\. Route 53 then responds to queries using each record based on the ratio of a record's weight to the total\.

  For example, if two weighted records have weights of 10 and 20, the total is 30\. On average, Route 53 responds to DNS queries with the value in the first record 1/3rd of the time \(10/30\) and the value in the second record 2/3rds of the time \(20/30\)\. 

  To disable routing to a resource, set **Weight** for that record to **0**\. If you set **Weight** to **0** for all the weighted records that have the same name and type, traffic is routed to all resources with equal probability\. This ensures that you don't accidentally disable routing for a group of weighted records\.

  The effect of setting **Weight** to **0** is different when you associate health checks with weighted records\. For more information, see [How Amazon Route 53 chooses records when health checking is configured](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-how-route-53-chooses-records.html)\.
+ **Value/Route traffic to**: Choose the applicable value:
  + **To route traffic to an AWS resource that appears in the list**: choose the type of the resource, such as a CloudFront distribution or an Amazon S3 website endpoint\. Then specify the applicable values, such as the AWS Region where you created the resource, and the resource that you want to route traffic to\.
  + **To route traffic to a type of AWS resource that isn't listed**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
  + **To create other types of records, such as TXT records**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
+ **Health check**: If you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy, choose a health check\. 

## Learn more<a name="routing-weighted-learn-more"></a>
+ [Working with records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)