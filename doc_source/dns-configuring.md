# Configuring Amazon Route 53 as Your DNS Service<a name="dns-configuring"></a>

You can use Amazon Route 53 as the DNS service for your domain, such as example\.com\. When Route 53 is your DNS service, it routes internet traffic to your website by translating friendly domain names like www\.example\.com into numeric IP addresses, like 192\.0\.2\.1, that computers use to connect to each other\. When someone types your domain name in a browser or sends you an email, a DNS query is forwarded to Route 53, which responds with the appropriate value\. For example, Route 53 might respond with the IP address for the web server for example\.com\.

In this chapter, we explain how to configure Route 53 to route your internet traffic to the right places\. We also explain how to migrate DNS service to Route 53 if you're currently using another DNS service, and how to use Route 53 as the DNS service for a new domain\. 


+ [Making Amazon Route 53 the DNS Service for an Existing Domain](MigratingDNS.md)
+ [Configuring DNS Routing for a New Domain](dns-configuring-new-domain.md)
+ [Routing Traffic to Your Resources](dns-routing-traffic-to-resources.md)
+ [Working with Hosted Zones](hosted-zones-working-with.md)
+ [Working with Records](rrsets-working-with.md)
+ [Using Auto Naming to Create Records and Health Checks](autonaming.md)
+ [Using Traffic Flow to Route DNS Traffic](traffic-flow.md)
+ [DNS Constraints and Behaviors](DNSBehavior.md)