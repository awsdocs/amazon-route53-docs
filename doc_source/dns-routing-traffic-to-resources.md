# Routing Traffic to Your Resources<a name="dns-routing-traffic-to-resources"></a>

When users request your website or web application, for example, by entering the name of your domain in a web browser, Amazon Route 53 helps to route users to your resources, such as an Amazon S3 bucket or a web server in your data center\. To configure Route 53 to route traffic to your resources, you do the following:

1. Create a hosted zone\. You can create either a public hosted zone or a private hosted zone:  
**Public hosted zone**  
Create a public hosted zone if you want to route internet traffic to your resources, for example, so your customers can view the company website that you're hosting on EC2 instances\. For more information, see [Working with Public Hosted Zones](AboutHZWorkingWith.md)\.  
**Private hosted zone**  
Create a private hosted zone if you want to route traffic within an Amazon VPC\. For more information, see [Working with Private Hosted Zones](hosted-zones-private.md)\.

1. Create records in the hosted zone\. Records define where you want to route traffic for each domain name or subdomain name\. For example, to route traffic for www\.example\.com to a web server in your data center, you typically create a www\.example\.com record in the example\.com hosted zone\. 

   For more information, see the following topics:
   + [Working with Records](rrsets-working-with.md)
   + [Routing Traffic for Subdomains](dns-routing-traffic-for-subdomains.md)
   + [Routing Internet Traffic to Your AWS Resources](routing-to-aws-resources.md)