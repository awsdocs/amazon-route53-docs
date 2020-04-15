# Integration with other services<a name="integration-with-other-services"></a>

You can integrate Amazon Route 53 with other AWS services to log requests that are sent to the Route 53 API, monitor the status of your resources, and assign tags to your resources\. In addition, you can use Route 53 to route internet traffic to your AWS resources\.

**Topics**
+ [Logging, monitoring, and tagging](#integration-logging-monitoring-tagging)
+ [Routing traffic to other AWS resources](#integration-routing-traffic)

## Logging, monitoring, and tagging<a name="integration-logging-monitoring-tagging"></a>

**AWS CloudTrail**  
Amazon Route 53 is integrated with AWS CloudTrail, a service that captures information about every request that is sent to the Route 53 API by your AWS account\. You can use information in the CloudTrail log files to determine which requests were made to Route 53, the source IP address from which each request was made, who made the request, when it was made, and so on\.  
For more information, see [Logging Amazon Route 53 API calls with AWS CloudTrail](logging-using-cloudtrail.md)\.

**Amazon CloudWatch**  
You can use Amazon CloudWatch to monitor the status—healthy or unhealthy—of your Route 53 health checks\. Health checks monitor the health and performance of your web applications, web servers, and other resources\. At regular intervals that you specify, Route 53 submits automated requests over the internet to your application, server, or other resource to verify that it's reachable, available, and functional\.  
For more information, see [Monitoring health checks using CloudWatch](monitoring-health-checks.md)\.

**Tag Editor**  
A tag is a label that you assign to an AWS resource, including Route 53 domains, hosted zones, and health checks\. Each tag consists of a key and a value, both of which you define\. For example, you might assign a tag to a domain registration that has the key "Customer" and the value "Example Corp\." You can use tags for a variety of purposes; one common use is to categorize and track your AWS costs\.  
For more information, see [Tagging Amazon Route 53 resources](tagging-resources.md)\.

## Routing traffic to other AWS resources<a name="integration-routing-traffic"></a>

You can use Amazon Route 53 to route traffic to a variety of AWS resources\.

**Amazon API Gateway**  
Amazon API Gateway lets you create, publish, maintain, monitor, and secure APIs at any scale\. You can create APIs that access AWS or other web services, as well as data stored in the AWS Cloud\.  
You can use Route 53 to route traffic to an API Gateway API\. For more information, see [Routing traffic to an Amazon API Gateway API by using your domain name](routing-to-api-gateway.md)\.

**Amazon CloudFront**  
To speed up delivery of your web content, you can use Amazon CloudFront, the AWS content delivery network \(CDN\)\. CloudFront can deliver your entire website—including dynamic, static, streaming, and interactive content—by using a global network of edge locations\. CloudFront routes requests for your content to the edge location that gives your users the lowest latency\. You can use Route 53 to route traffic for your domain to your CloudFront distribution\. For more information, see [Routing traffic to an Amazon CloudFront web distribution by using your domain name](routing-to-cloudfront-distribution.md)\.

**Amazon EC2**  
Amazon EC2 provides scalable computing capacity in the AWS Cloud\. You can launch an EC2 virtual computing environment \(an instance\) using a preconfigured template \(an Amazon Machine Image, or AMI\)\. When you launch an EC2 instance, EC2 automatically installs the operating system \(Linux or Microsoft Windows\) and additional software included in the AMI, such as web server or database software\.  
If you host a website or run a web application on an EC2 instance, you can route traffic for your domain, such as example\.com, to your server by using Route 53\. For more information, see [Routing traffic to an Amazon EC2 instance](routing-to-ec2-instance.md)\.

**AWS Elastic Beanstalk**  
If you use AWS Elastic Beanstalk to deploy and manage applications in the AWS Cloud, you can use Route 53 to route DNS traffic for your domain, such as example\.com, to an Elastic Beanstalk environment\. For more information, see [Routing traffic to an AWS Elastic Beanstalk environment](routing-to-beanstalk-environment.md)\.

**Elastic Load Balancing**  
If you host a website on multiple Amazon EC2 instances, you can distribute traffic to your website across the instances by using an Elastic Load Balancing \(ELB\) load balancer\. The ELB service automatically scales the load balancer as traffic to your website changes over time\. The load balancer also can monitor the health of its registered instances and route domain traffic only to healthy instances\.   
You can use Route 53 to route traffic for your domain to your Classic, Application, or Network Load Balancer\. For more information, see [Routing traffic to an ELB load balancer](routing-to-elb-load-balancer.md)\.

**Amazon Lightsail**  
Amazon Lightsail provides compute, storage, and networking capacity and capabilities to deploy and manage websites, web applications, and databases in the cloud for a low, predictable monthly price\.  
If you use Lightsail, you can use Route 53 to route traffic to your Lightsail instance\. For more information, see [Using Route 53 to point a domain to an Amazon Lightsail instance](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-using-route-53-to-point-a-domain-to-an-instance)\.

**Amazon RDS**  
If you use an Amazon RDS database instance for data storage for your web application, the domain name that is assigned to your DB instance is a long, partially random, alphanumeric string, such as `myexampledb.a1b2c3d4wxyz.us-west-2.rds.amazonaws.com`\. If you want to use a domain name that's easier to remember, you can use Route 53 to associate your domain name, such as `productdata.example.com`, with the domain name of your DB instance\. For more information, see [Opening connections to an Amazon RDS database instance using your domain name](routing-to-rds-db.md)\.

**Amazon S3**  
Amazon Simple Storage Service \(Amazon S3\) provides secure, durable, highly scalable cloud storage\. You can configure an S3 bucket to host a static website that can include web pages and client\-side scripts\. \(S3 doesn't support server\-side scripting\.\) You can use Route 53 to route traffic to an Amazon S3 bucket\. For more information, see the following topics:  
+ For information about routing traffic to a bucket, see [Routing traffic to a website that is hosted in an Amazon S3 bucket](RoutingToS3Bucket.md)\.
+ For a more detailed explanation of how to host a static website in an S3 bucket, see [Getting started with Amazon Route 53](getting-started.md)\.

**Amazon Virtual Private Cloud \(Amazon VPC\)**  
An interface endpoint lets you connect to services that are powered by AWS PrivateLink\. These services include some AWS services, services hosted by other AWS customers and partners in their own VPCs \(referred to as *endpoint services*\), and supported AWS Marketplace partner services\.  
You can use Route 53 to route traffic to an interface endpoint\. For more information, see [Routing traffic to an Amazon Virtual Private Cloud interface endpoint by using your domain name](routing-to-vpc-interface-endpoint.md)\.

**Amazon WorkMail**  
If you're using Amazon WorkMail for your business email and you're using Route 53 as your DNS service, you can use Route 53 to route traffic to your Amazon WorkMail email domain\. For more information, see [Routing traffic to Amazon WorkMail](routing-to-workmail.md)\.