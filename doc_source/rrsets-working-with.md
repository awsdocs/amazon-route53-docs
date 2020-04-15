# Working with records<a name="rrsets-working-with"></a>

After you create a hosted zone for your domain, such as example\.com, you create records to tell the Domain Name System \(DNS\) how you want traffic to be routed for that domain\.

For example, you might create records that cause DNS to do the following:
+ Route internet traffic for example\.com to the IP address of a host in your data center\.
+ Route email for that domain \(ichiro@example\.com\) to a mail server \(mail\.example\.com\)\.
+ Route traffic for a subdomain called operations\.tokyo\.example\.com to the IP address of a different host\. 

Each record includes the name of a domain or a subdomain, a record type \(for example, a record with a type of MX routes email\), and other information applicable to the record type \(for MX records, the host name of one or more mail servers and a priority for each server\)\. For information about the different record types, see [Supported DNS record types](ResourceRecordTypes.md)\.

The name of each record in a hosted zone must end with the name of the hosted zone\. For example, the example\.com hosted zone can contain records for www\.example\.com and accounting\.tokyo\.example\.com subdomains, but cannot contain records for a www\.example\.ca subdomain\. 

**Note**  
To create records for complex routing configurations, you can also use the traffic flow visual editor and save the configuration as a traffic policy\. You can then associate the traffic policy with one or more domain names \(such as example\.com\) or subdomain names \(such as www\.example\.com\), in the same hosted zone or in multiple hosted zones\. In addition, you can roll back the updates if the new configuration isn't performing as you expected it to\. For more information, see [Using traffic flow to route DNS traffic](traffic-flow.md)\.

Amazon Route 53 doesn't charge for the records that you add to a hosted zone\. For information about the maximum number of records that you can create in a hosted zone, see [Quotas](DNSLimitations.md)\. 

**Topics**
+ [Choosing a routing policy](routing-policy.md)
+ [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)
+ [Supported DNS record types](ResourceRecordTypes.md)
+ [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)
+ [Values that you specify when you create or edit Amazon Route 53 records](resource-record-sets-values.md)
+ [Creating records by importing a zone file](resource-record-sets-creating-import.md)
+ [Editing records](resource-record-sets-editing.md)
+ [Deleting records](resource-record-sets-deleting.md)
+ [Listing records](resource-record-sets-listing.md)