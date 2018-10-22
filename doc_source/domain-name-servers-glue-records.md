# Adding or Changing Name Servers and Glue Records for a Domain<a name="domain-name-servers-glue-records"></a>

When you register a domain with Route 53, we automatically create a hosted zone for the domain, assign four name servers to the hosted zone, and then update the domain registration to use those name servers\. You typically don't need to change those settings unless you want to use another DNS service or you want to use white\-label name servers\.

**Warning**  
If you change name servers to the wrong values, specify the wrong IP addresses in glue records, or delete one or more name servers without specifying new ones, your website or application might become unavailable on the internet\.

**If you want to use another DNS service**  
If you want to use a DNS service other than Route 53 for your domain, use the following procedure to change the name servers for the domain registration to the name servers that are provided by the other DNS service\.  
If you change name servers and Route 53 returns the following error message, the registry for the TLD doesn't recognize the name servers that you specified as valid name servers:  
`"We're sorry to report that the operation failed after we forwarded your request to our registrar partner. This is because: One or more of the specified nameservers are not known to the domain registry."`  
TLD registries commonly support name servers provided by public DNS services but don't support private DNS servers, such as DNS servers that you configured on Amazon EC2 instances, unless the registry has IP addresses for those name servers\. Route 53 doesn't support using name servers that aren't recognized by the TLD registry\. If you encounter this error, you must change to name servers for Route 53 or another public DNS service\.

**If you want to use white\-label name servers**  
If you want the names of your name servers to be subdomains of your domain name, you can create white\-label name servers\. \(White\-label name servers are also known as vanity name servers or private name servers\.\) For example, you might create name servers ns1\.example\.com through ns4\.example\.com for the domain example\.com\. To use white\-label name servers, use the following procedure to specify the IP addresses of your name servers instead of the names\. These IP addresses are known as glue records\.  
For more information about configuring white\-label name servers, see [Configuring White\-Label Name Servers](white-label-name-servers.md)\.

**To add or change name servers and glue records for a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain for which you want to edit settings\.

1. Choose **Add/Edit Name Servers**\.

1. In the **Edit Name Servers** dialog box, you can do the following:

   + Add one or more name servers\.

   + Replace the name of an existing name server\.

   + Add glue records or change the IP addresses in glue records\. If you add a name server or change the name of a name server and specify a name that is a subdomain of the domain that you're updating \(for example, ns1\.example\.com in the domain example\.com\), Route 53 prompts you to specify one or more IP addresses for the name server\. These IP addresses are known as glue records\.

     You can enter addresses in IPv4 or IPv6 format\. If a name server has multiple IP addresses, enter each address on a separate line\.

   + Delete a name server\. Choose the x icon on the right side of the field for that name server\.

1. Choose **Update**\.