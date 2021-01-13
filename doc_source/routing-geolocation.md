# Geolocation records to add to *domain\-name*<a name="routing-geolocation"></a>

Each geolocation record that you define has the same name, type, and TTL that you specified in **Basic configuration**\. In addition, each record has the following values:
+ **Record ID**: When you create records that have a routing policy other than simple, enter a value that uniquely identifies each record that has the same name and type\. For example, you might assign a date/time stamp or a sequential counter\. 
+ **Location**: When you configure Route 53 to respond to DNS queries based on the location that the queries originated from, choose the continent, country, or United States state for which you want Route 53 to respond with the settings in this record\.
**Note**  
We recommend that you create one geolocation record that has a value of **Default** for **Location**\. This record covers geographic locations that you haven't created records for and DNS queries that Route 53 can't identify a location for\.
+ **Value/Route traffic to**: Choose the applicable value:
  + **To route traffic to an AWS resource that appears in the list**: choose the type of the resource, such as a CloudFront distribution or an Amazon S3 website endpoint\. Then specify the applicable values, such as the AWS Region where you created the resource, and the resource that you want to route traffic to\.
  + **To route traffic to a type of AWS resource that isn't listed**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
  + **To create other types of records, such as TXT records**: choose **IP address or another value depending on the record type**\. Then specify the applicable value, such as an Amazon EC2 Elastic IP address\.
+ **Health check**: If you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy, choose a health check\. 

## Learn more<a name="routing-geolocation-learn-more"></a>
+ [Working with records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)