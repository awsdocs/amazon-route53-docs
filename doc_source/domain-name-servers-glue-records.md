# Adding or changing name servers and glue records for a domain<a name="domain-name-servers-glue-records"></a>

When you register a domain with Route 53, we automatically create a hosted zone for the domain, assign four name servers to the hosted zone, and then update the domain registration to use those name servers\. You typically don't need to change those settings unless you want to use another DNS service or you want to use white\-label name servers\.

**Warning**  
If you change name servers to the wrong values, specify the wrong IP addresses in glue records, or delete one or more name servers without specifying new ones, your website or application might become unavailable on the internet for up to two days\.

**Topics**
+ [Considerations for changing name servers and glue records](#domain-name-servers-glue-records-considerations)
+ [Adding or changing name servers or glue records](#domain-name-servers-glue-records-adding-changing)

## Considerations for changing name servers and glue records<a name="domain-name-servers-glue-records-considerations"></a>

Consider the following issues before you change your configuration\. 

**Topics**
+ [You want to make Route 53 the DNS service for your domain](#updating-name-servers-route-53)
+ [You want to use another DNS service](#updating-name-servers-other-dns-service)
+ [You want to use white-label name servers](#updating-name-servers-white-label)
+ [You're changing name servers for a .it domain](#updating-name-servers-it-domains)

**You want to make Route 53 the DNS service for your domain**  
If you're currently using another DNS service and you want to make Route 53 the DNS service for your domain, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md) for detailed instructions on how to migrate DNS service to Route 53\.   
If you don't rigorously follow the migration process, your domain can become unavailable on the internet for up to two days\.

**You want to use another DNS service**  
If you want to use a DNS service other than Route 53 for your domain, use the following procedure to change the name servers for the domain registration to the name servers that are provided by the other DNS service\.  
If you change name servers and Route 53 returns the following error message, the registry for the TLD doesn't recognize the name servers that you specified as valid name servers:  
`"We're sorry to report that the operation failed after we forwarded your request to our registrar associate. This is because: One or more of the specified nameservers are not known to the domain registry."`  
TLD registries commonly support name servers provided by public DNS services but don't support private DNS servers, such as DNS servers that you configured on Amazon EC2 instances, unless the registry has IP addresses for those name servers\. Route 53 doesn't support using name servers that aren't recognized by the TLD registry\. If you encounter this error, you must change to name servers for Route 53 or another public DNS service\.

**You want to use white\-label name servers**  
If you want the names of your name servers to be subdomains of your domain name, you can create white\-label name servers\. \(White\-label name servers are also known as vanity name servers or private name servers\.\) For example, you might create name servers ns1\.example\.com through ns4\.example\.com for the domain example\.com\. To use white\-label name servers, use the following procedure to specify the IP addresses of your name servers instead of the names\. These IP addresses are known as glue records\.  
For more information about configuring white\-label name servers, see [Configuring white\-label name servers](white-label-name-servers.md)\.

**You're changing name servers for a \.it domain**  
If you change name servers for a \.it domain, the registry for \.it domains performs a check to confirm that the name servers are valid\. If you specify the wrong name servers and the check fails, the registry continues to check for five days\. During this time, you can't update the names of the name servers to correct the error because the EPP status code is `pendingUpdate`\. The registry continues to respond to DNS queries using the name servers from before you made the change\. If the previous name servers are no longer available, your domain becomes unavailable on the internet\.  
Whenever you change name servers for a domain, confirm that DNS is responding to queries with the new name servers before you cancel the old DNS service or you delete the Route 53 hosted zone that used the old name servers\.
For information about getting help from AWS to correct the names of your name servers with the registry for \.it domains, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

## Adding or changing name servers or glue records<a name="domain-name-servers-glue-records-adding-changing"></a>

To add or change name servers or glue records, perform the following procedure\.

**Note**  
By default, DNS resolvers typically cache the names of name servers for two days\. As a result, your changes can take two days to take effect\. For more information, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\. <a name="domain-name-servers-glue-records-adding-changing-procedure"></a>

**To add or change name servers or glue records for a domain**

1. Review [Considerations for changing name servers and glue records](#domain-name-servers-glue-records-considerations) and address the applicable issues, if any\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain for which you want to edit settings\.

1. Choose **Add/Edit Name Servers**\.

1. In the **Edit Name Servers** dialog box, you can do the following:
   + Change the DNS service for the domain by doing one of the following:
     + Replace the name servers for another DNS service with the name servers for a Route 53 hosted zone
     + Replace the name servers for a Route 53 hosted zone with the name servers for another DNS service
     + Replace the name servers for one Route 53 hosted zone with the name servers for a different Route 53 hosted zone

     For information about changing the DNS service for a domain, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\. For information about getting the name servers for the Route 53 hosted zone that you want to use for DNS service for the domain, see [Getting the name servers for a public hosted zone](GetInfoAboutHostedZone.md)\.
   + Add one or more name servers\.
   + Replace the name of an existing name server\.
   + If you specify white\-label name servers, add or change the IP addresses in glue records\. You can enter addresses in IPv4 or IPv6 format\. If a name server has multiple IP addresses, enter each address on a separate line\.

     A white\-label name server includes your domain name, such as example\.com, in the name of the name server, such as ns1\.example\.com\. When you specify a white\-label name server, Route 53 prompts you to specify one or more IP addresses for the name server\. The IP address is known as a glue record\. For more information, see [Configuring white\-label name servers](white-label-name-servers.md)\.
   + Delete a name server\. Choose the x icon on the right side of the field for that name server\.
**Warning**  
If you change name servers to the wrong values, specify the wrong IP addresses in glue records, or delete one or more name servers without specifying new ones, your website or application might become unavailable on the internet for up to two days\.

1. Choose **Update**\.

1. If you encounter issues while adding or changing name servers or glue records, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.