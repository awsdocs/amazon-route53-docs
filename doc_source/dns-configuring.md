# Configuring Amazon Route 53 as your DNS service<a name="dns-configuring"></a>

You can use Amazon Route 53 as the DNS service for your domain, such as example\.com\. When Route 53 is your DNS service, it routes internet traffic to your website by translating friendly domain names like www\.example\.com into numeric IP addresses, like 192\.0\.2\.1, that computers use to connect to each other\. When someone types your domain name in a browser or sends you an email, a DNS query is forwarded to Route 53, which responds with the appropriate value\. For example, Route 53 might respond with the IP address for the web server for example\.com\.

In this chapter, we explain how to configure Route 53 to route your internet traffic to the right places\. We also explain how to migrate DNS service to Route 53 if you're currently using another DNS service, and how to use Route 53 as the DNS service for a new domain\. 

**Topics**
+ [Making Amazon Route 53 the DNS service for an existing domain](MigratingDNS.md)
+ [Configuring DNS routing for a new domain](dns-configuring-new-domain.md)
+ [Routing traffic to your resources](dns-routing-traffic-to-resources.md)
+ [Working with hosted zones](hosted-zones-working-with.md)
+ [Working with records](rrsets-working-with.md)
+ [Using traffic flow to route DNS traffic](traffic-flow.md)
+ [Using AWS Cloud Map to create records and health checks](autonaming.md)
+ [DNS constraints and behaviors](DNSBehavior.md)