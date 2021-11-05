# Configuring DNS routing for a new domain<a name="dns-configuring-new-domain"></a>

When you register a domain with Route 53, we automatically make Route 53 the DNS service for the domain\. Route 53 creates a hosted zone that has the same name as the domain, assigns four name servers to the hosted zone, and updates the domain to use those name servers\.

To specify how you want Route 53 to route internet traffic for the domain, you create records in the hosted zone\. For example, if you want to route requests for example\.com to a web server that's running on an Amazon EC2 instance, you create a record in the example\.com hosted zone, and you specify the Elastic IP address for the EC2 instance\. For more information, see the following topics:
+ For information about how to create records in your hosted zone, see [Working with records](rrsets-working-with.md)\.
+ For information about how to route traffic to selected AWS resources, see [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.
+ For information about how DNS works, see [How internet traffic is routed to your website or web application](welcome-dns-service.md)\.