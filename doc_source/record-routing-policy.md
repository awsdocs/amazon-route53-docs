# Choose routing policy<a name="record-routing-policy"></a>

Routing policies let you choose how Route 53 routes traffic to you resources\. If you have multiple resources that perform the same operation, such as serve content for a website, choose a routing policy other than simple\. Here's a brief comparison:
+ **Simple**: Simple records use standard DNS functionality\. 
+ **Weighted**: Weighted records let you specify what portion of traffic to send to each resource\. 
+ **Geolocation**: Geolocation records let you route traffic to your resources based on the geographic location of your users\.
+ **Latency**: Latency records let you route traffic to resources in the AWS Region that provides the lowest latency\. All resources must be in AWS Regions\. 
+ **Failover**: Failover records let you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy\. 
+ **Multivalue answer**: Multivalue answer records let you configure Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries\. 

## Learn more<a name="record-routing-policy-learn-more"></a>
+ [Choosing a routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)