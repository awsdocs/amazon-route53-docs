# Failover records to add to *domain\-name*<a name="routing-failover"></a>

Each failover record that you define has the same name, type, and TTL that you specified in **Basic configuration**\. In addition, each record has the following values:
+ **Record ID**: When you create records that have a routing policy other than simple, enter a value that uniquely identifies each record that has the same name and type\. For example, you might assign a date/time stamp or a sequential counter\. 
+ **Failover record type**: Traffic is routed to the resource that you specify for the primary record when the resource is healthy\. Traffic is routed to the resource that you specify for the secondary record when the resource for the primary record is unhealthy\.
+ **Value/Route traffic to**: Choose the applicable value:
  + **To route traffic to an AWS resource that appears in the list**: choose the type of the resource, such as a CloudFront distribution or an Amazon S3 website endpoint\. Then specify the applicable values, such as the AWS Region where you created the resource, and the resource that you want to route traffic to\.
  + **To route traffic to a type of AWS resource that isn't listed**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
  + **To create other types of records, such as TXT records**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
+ **Health check**: If you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy, choose a health check\. 

## Learn more<a name="routing-failover-learn-more"></a>
+ [Working with records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)