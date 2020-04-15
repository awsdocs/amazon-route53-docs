# What is Amazon Route 53?<a name="Welcome"></a>

Amazon Route 53 is a highly available and scalable Domain Name System \(DNS\) web service\. You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking\. If you choose to use Route 53 for all three functions, perform the steps in this order:

**1\. Register domain names**  
Your website needs a name, such as example\.com\. Route 53 lets you register a name for your website or web application, known as a *domain name*\.  
+ For an overview, see [How domain registration works](welcome-domain-registration.md)\.
+ For a procedure, see [Registering a new domain](domain-register.md)\.
+ For a tutorial that takes you through registering a domain and creating a simple website in an Amazon S3 bucket, see [Getting started with Amazon Route 53](getting-started.md)\.

**2\. Route internet traffic to the resources for your domain**  
When a user opens a web browser and enters your domain name \(example\.com\) or subdomain name \(acme\.example\.com\) in the address bar, Route 53 helps connect the browser with your website or web application\.  
+ For an overview, see [How internet traffic is routed to your website or web application](welcome-dns-service.md)\.
+ For procedures, see [Configuring Amazon Route 53 as your DNS service](dns-configuring.md)\.

**3\. Check the health of your resources**  
Route 53 sends automated requests over the internet to a resource, such as a web server, to verify that it's reachable, available, and functional\. You also can choose to receive notifications when a resource becomes unavailable and choose to route internet traffic away from unhealthy resources\.   
+ For an overview, see [How Amazon Route 53 checks the health of your resources](welcome-health-checks.md)\.
+ For procedures, see [Creating Amazon Route 53 health checks and configuring DNS failover](dns-failover.md)\. 

**Topics**
+ [How domain registration works](welcome-domain-registration.md)
+ [How internet traffic is routed to your website or web application](welcome-dns-service.md)
+ [How Amazon Route 53 checks the health of your resources](welcome-health-checks.md)
+ [Amazon Route 53 concepts](route-53-concepts.md)
+ [How to get started with Amazon Route 53](welcome-how-to-get-started.md)
+ [Related services](welcome-related-services.md)
+ [Accessing Amazon Route 53](welcome-accessing-route-53.md)
+ [AWS Identity and Access Management](IAMRoute53.md)
+ [Amazon Route 53 pricing and billing](Route53Pricing.md)