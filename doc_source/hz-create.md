# Create hosted zone<a name="hz-create"></a>

You create a hosted zone when you want to use Route 53 to route internet traffic for your domain or to route traffic within your VPCs\. Then you create records in the hosted zone for the domain name \(example\.com\) and subdomains \(such as www\.example\.com or blog\.example\.com\)\. 

For example, suppose you have a web server that serves content for your example\.com website\. You create a public hosted zone named example\.com\. Then you create records named **example\.com** and **www\.example\.com**\. In each record, you specify the IP address of the web server, for example, 192\.0\.2\.44\. 

When someone opens a web browser and enters **example\.com** or **www\.example\.com**, the browser gets the IP address for your web server from the corresponding Route 53 record\. The browser then gets your website content from your web server at 192\.0\.2\.44\. 

## Learn more<a name="hz-create-learn-more"></a>
+ [Working with public hosted zones](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/AboutHZWorkingWith.html)
+ [Working with private hosted zones](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zones-private.html)
+ [How internet traffic is routed to your website or web application](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/welcome-dns-service.html)