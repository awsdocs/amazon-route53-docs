# Creating a public hosted zone<a name="CreatingHostedZone"></a>

A public hosted zone is a container that holds information about how you want to route traffic on the internet for a specific domain, such as example\.com, and its subdomains \(acme\.example\.com, zenith\.example\.com\)\. After you create a hosted zone, you create records that specify how you want to route traffic for the domain and subdomains\.

**Important**  
You can create a hosted zone only for a domain that you have permission to administer\. Typically, this means that you own the domain, but you might also be developing an application for the domain registrant\.

**To create a public hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get Started Now** under **DNS Management**\. On the next page, choose **Create Hosted Zone**\.

   If you're already using Route 53, choose **Hosted zones** in the navigation pane\.

1. Choose **Create Hosted Zone**\.

1. In the **Create Hosted Zone** pane, enter the name of the domain that you want to route traffic for\. You can also optionally enter a comment\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

1. For **Type**, accept the default value of **Public Hosted Zone**\.

1. Choose **Create**\.

1. Create records that specify how you want to route traffic for the domain and subdomains\. For more information, see [Working with records](rrsets-working-with.md)\.

1. To use records in the new hosted zone to route traffic for your domain, see the applicable topic:
   + If you're making Route 53 the DNS service for a domain that is registered with another domain registrar, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.
   + If the domain is registered with Route 53, see [Adding or changing name servers and glue records for a domain](domain-name-servers-glue-records.md)\.