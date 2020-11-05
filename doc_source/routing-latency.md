# Latency records to add to *domain\-name*<a name="routing-latency"></a>

Each latency record that you define has the same name, type, and TTL that you specified in **Basic configuration**\. In addition, each record has the following values:
+ **Record ID**: When you create records that have a routing policy other than simple, enter a value that uniquely identifies each record that has the same name and type\. For example, you might assign a date/time stamp or a sequential counter\. 
+ **Region**: The Amazon EC2 Region where the resource that you specified in this record resides\. Route 53 recommends an Amazon EC2 Region based on other values that you've specified\. We recommend that you not change this value\.

  Note the following:
  + You can only create one latency record for each Amazon EC2 Region\.
  + You aren't required to create latency records for all Amazon EC2 Regions\. Route 53 chooses the Region with the best latency from among the Regions that you create latency records for\.
  + If you create a record tagged with the Region **cn\-north\-1**, Route 53 always responds to queries from within China using this record, regardless of the latency\.
+ **Value/Route traffic to**: Choose the applicable value:
  + **To route traffic to an AWS resource that appears in the list**: choose the type of the resource, such as a CloudFront distribution or an Amazon S3 website endpoint\. Then specify the applicable values, such as the AWS Region where you created the resource, and the resource that you want to route traffic to\.
  + **To route traffic to a type of AWS resource that isn't listed**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
  + **To create other types of records, such as TXT records**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
+ **Health check**: If you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy, choose a health check\. 

## Learn more<a name="routing-latency-learn-more"></a>
+ [Working with Records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)