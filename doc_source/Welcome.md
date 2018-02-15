# What Is Amazon Route 53?<a name="Welcome"></a>

You can use Amazon Route 53 to help you get a website or web application up and running\. Route 53 performs three main functions:

+ **Register domain names** – Your website needs a name, such as example\.com\. Route 53 lets you register a name for your website or web application, known as a *domain name*\. For an overview, see [How Domain Registration Works](welcome-domain-registration.md)\.

+ **Route internet traffic to the resources for your domain** – When a user opens a web browser and enters your domain name in the address bar, Route 53 helps the Domain Name System \(DNS\) connect the browser with your website or web application\. For an overview, see [How Internet Traffic Is Routed to Your Website or Web Application](welcome-dns-service.md)\.

+ **Check the health of your resources** – Route 53 sends automated requests over the internet to a resource, such as a web server, to verify that it's reachable, available, and functional\. You also can choose to receive notifications when a resource becomes unavailable and choose to route internet traffic away from unhealthy resources\. For an overview, see [How Amazon Route 53 Checks the Health of Your Resources](welcome-health-checks.md)\.

You can use any combination of these functions\. For example, you can use Route 53 both to register your domain name and to route internet traffic for the domain, or you can use Route 53 to route internet traffic for a domain that you registered with another domain registrar\. If you choose to use Route 53 for all three functions, you register your domain name, then configure Route 53 to route internet traffic for your domain, and finally configure Route 53 to check the health of your resources\.


+ [How Domain Registration Works](welcome-domain-registration.md)
+ [How Internet Traffic Is Routed to Your Website or Web Application](welcome-dns-service.md)
+ [How Amazon Route 53 Checks the Health of Your Resources](welcome-health-checks.md)
+ [Amazon Route 53 Concepts](route-53-concepts.md)
+ [How to Get Started with Amazon Route 53](welcome-how-to-get-started.md)
+ [Related Services](welcome-related-services.md)
+ [Accessing Amazon Route 53](welcome-accessing-route-53.md)
+ [AWS Identity and Access Management](IAMRoute53.md)
+ [Amazon Route 53 Pricing](Route53Pricing.md)
+ [Amazon Route 53 and AWS Cloud Compliance](compliance.md)