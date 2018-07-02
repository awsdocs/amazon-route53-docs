# Creating a Public Hosted Zone<a name="CreatingHostedZone"></a>

A public hosted zone is a container that holds information about how you want to route traffic on the internet for a specific domain, such as example\.com, and its subdomains \(apex\.example\.com, acme\.example\.com\)\. After you create a hosted zone, you create records that specify how you want to route traffic for the domain and subdomains\.

**To create a hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Route 53, choose **Hosted zones** in the navigation pane\.

1. Choose **Create Hosted Zone**\.

1. In the **Create Hosted Zone** pane, type the name of the domain that you want to route traffic for\. You can also optionally type a comment\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

1. For **Type**, accept the default value of **Public Hosted Zone**\.

1. Choose **Create**\.

1. Create records that specify how you want to route traffic for the domain and subdomains\. For more information, see [Working with Records](rrsets-working-with.md)\.

1. To use records in the new hosted zone to route traffic for your domain, see the applicable topic:

   + If you're making Route 53 the DNS service for a domain that is registered with another domain registrar, see [Making Amazon Route 53 the DNS Service for an Existing DomainMaking Route 53 the DNS Service for an Existing Domain](MigratingDNS.md)\.

   + If the domain is registered with Route 53, see [Adding or Changing Name Servers and Glue Records for a Domain](domain-name-servers-glue-records.md)\.