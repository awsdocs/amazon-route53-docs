# Configuring Amazon Route 53 as Your DNS Service<a name="dns-configuring"></a>

You can use Amazon Route 53 as the DNS service for your domain, such as example\.com\. When Amazon Route 53 is your DNS service, it routes internet traffic to your website by translating friendly domain names like www\.example\.com into numeric IP addresses, like 192\.0\.2\.1, that computers use to connect to each other\. When someone enters your domain name in a browser or sends you email, a DNS query is forwarded to Amazon Route 53, which responds with the appropriate value, for example, the IP address for the web server for example\.com\.

In this chapter, we explain how to configure Amazon Route 53 to route your internet traffic to the right places\. We also explain how to migrate DNS service to Amazon Route 53 if you're currently using another DNS service\. 


+ [Migrating DNS Service for an Existing Domain to Amazon Route 53](MigratingDNS.md)
+ [Working with Public Hosted Zones](AboutHZWorkingWith.md)
+ [Working with Private Hosted Zones](hosted-zones-private.md)
+ [Working with Resource Record Sets](rrsets-working-with.md)
+ [Using Traffic Flow to Route DNS Traffic](traffic-flow.md)
+ [Using Amazon Route 53 as the DNS Service for Subdomains Without Migrating the Parent Domain](creating-migrating.md)
+ [DNS Constraints and Behaviors](DNSBehavior.md)