# Creating records by importing a zone file<a name="resource-record-sets-creating-import"></a>

If you're migrating from another DNS service provider, and if your current DNS service provider lets you export your current DNS settings to a zone file, you can quickly create all of the records for an Amazon Route 53 hosted zone by importing a zone file\.

**Note**  
A zone file uses a standard format known as BIND to represent records in a text format\. For information about the format of a zone file, see the Wikipedia entry [Zone file](https://en.wikipedia.org/wiki/Zone_file)\. Additional information is available in [RFC 1034, Domain Names—Concepts and Facilities](http://tools.ietf.org/html/rfc1034) section 3\.6\.1, and [RFC 1035, Domain Names—Implementation and Specification](http://tools.ietf.org/html/rfc1035) section 5\. 

If you want to create records by importing a zone file, note the following:
+ The zone file must be in RFC\-compliant format\.
+ The hosted zone must be empty except for the default NS and SOA records\.
+ The domain name of the records in the zone file must match the name of the hosted zone\.
+ Route 53 supports the `$ORIGIN` and `$TTL` keywords\. If the zone file includes `$GENERATE` or `$INCLUDE` keywords, the import fails and Route 53 returns an error\.
+ When you import the zone file, Route 53 ignores the SOA record in the zone file\. Route 53 also ignores any NS records that have the same name as the hosted zone\.
+ You can import a maximum of 1000 records\. If you need to import more than 1000 records, you might be able to use the [BIND to Amazon Route 53 Conversion Tool](https://aws.amazon.com/code/4495891528591897)\.
+ We recommend that you review the contents of the zone file to confirm that record names include or exclude a trailing dot as appropriate:
  + When the name of a record in the zone file includes a trailing dot \(`example.com.`\), the import process interprets the name as a fully qualified domain name and creates a Route 53 record with that name\.
  + When the name of a record in the zone file does not include a trailing dot \(`www`\), the import process concatenates that name with the domain name in the zone file \(`example.com`\) and creates a Route 53 record with the concatenated name \(`www.example.com`\)\.

  If the export process doesn't add a trailing dot to the fully qualified domain names of a record, the Route 53 import process adds the domain name to the name of the record\. For example, suppose you're importing records into the hosted zone `example.com` and the name of an MX record in the zone file is `mail.example.com`, with no trailing dot\. The Route 53 import process creates an MX record named `mail.example.com.example.com`\.
**Important**  
For CNAME, MX, PTR, and SRV records, this behavior also applies to the domain name that is included in the RDATA value\. For example, suppose you have a zone file for `example.com`\. If a CNAME record in the zone file \(`support`, without a trailing dot\) has an RDATA value of `www.example.com` \(also without a trailing dot\), the import process creates a Route 53 record with the name `support.example.com` that routes traffic to `www.example.com.example.com`\. Before you import your zone file, review RDATA values and update as applicable\. 

Route 53 doesn't support exporting records to a zone file\.<a name="RRSchanges_import_console_procedure"></a>

**To create records by importing a zone file**

1. Get a zone file from the DNS service provider that is currently servicing the domain\. The process and terminology vary from one service provider to another\. Refer to your provider's interface and documentation for information about exporting or saving your records in a zone file or a BIND file\.

   If the process isn't obvious, try asking your current DNS provider's customer support for your *records list* or *zone file* information\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. On the **Hosted Zones** page, create a new hosted zone:

   1. Choose **Create Hosted Zone**\.

   1. Enter the name of your domain and, optionally, a comment\. Note that the comment can't be edited later\.

   1. Choose **Create**\.

1. Choose **Import Zone File**\.

1. In the **Import Zone File** pane, paste the contents of your zone file into the **Zone File** text box\.

1. Choose **Import**\.
**Note**  
Depending on the number of records in your zone file, you might have to wait a few minutes for the records to be created\.

1. If you're using another DNS service for the domain \(which is common if you registered the domain with another registrar\), migrate DNS service to Route 53\. When that step is complete, your registrar will start to identify Route 53 as your DNS service in response to DNS queries for your domain, and the queries will start being sent to Route 53 DNS servers\. \(Typically, there's a day or two of delay before DNS queries start being routed to Route 53 because information about your previous DNS service is cached on DNS resolvers for that long\.\) For more information, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.