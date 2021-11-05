# Values that are common for all routing policies<a name="resource-record-sets-values-shared"></a>

These are the common values that you can specify when you create or edit Amazon Route 53 records\. These values are used by all routing policies\.



**Topics**
+ [Record name](#rrsets-values-common-name)
+ [Value/Route traffic to](#rrsets-values-common-value)
+ [TTL \(seconds\)](#rrsets-values-common-ttl)

## Record name<a name="rrsets-values-common-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

**CNAME records**  
If you're creating a record that has a value of **CNAME** for **Record type**, the name of the record can't be the same as the name of the hosted zone\.

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an asterisk \(\*\) in the names of hosted zones and records](DomainNameFormat.md#domain-name-format-asterisk)\.  
You can't use the \* wildcard for resource records sets that have a type of **NS**\.

## Value/Route traffic to<a name="rrsets-values-common-value"></a>

Choose **IP address or another value depending on the record type**\. Enter a value that is appropriate for the value of **Record type**\. For all types except **CNAME**, you can enter more than one value\. Enter each value on a separate line\.

**A — IPv4 address**  
An IP address in IPv4 format, for example, **192\.0\.2\.235**\.

**AAAA — IPv6 address**  
An IP address in IPv6 format, for example, **2001:0db8:85a3:0:0:8a2e:0370:7334**\.

**CAA — Certificate Authority Authorization**  
Three space\-separated values that control which certificate authorities are allowed to issue certificates or wildcard certificates for the domain or subdomain that is specified by **Record name**\. You can use CAA records to specify the following:  
+ Which certificate authorities \(CAs\) can issue SSL/TLS certificates, if any
+ The email address or URL to contact when a CA issues a certificate for the domain or subdomain

**CNAME — Canonical name**  
The fully qualified domain name \(for example, *www\.example\.com*\) that you want Route 53 to return in response to DNS queries for this record\. A trailing dot is optional; Route 53 assumes that the domain name is fully qualified\. This means that Route 53 treats *www\.example\.com* \(without a trailing dot\) and *www\.example\.com\.* \(with a trailing dot\) as identical\.

**MX — Mail exchange**  
A priority and a domain name that specifies a mail server, for example, **10 mailserver\.example\.com**\. The trailing dot is treated as optional\.

**NAPTR — Name Authority Pointer**  
Six space\-separated settings that are used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For more information, see [NAPTR record type](ResourceRecordTypes.md#NAPTRFormat)\.

**PTR — Pointer**  
The domain name that you want Route 53 to return\.

**NS — Name server**  
The domain name of a name server, for example, **ns1\.example\.com**\.  
You can specify an NS record with only simple routing policy\.

**SPF — Sender Policy Framework**  
An SPF record enclosed in quotation marks, for example, **"v=spf1 ip4:192\.168\.0\.1/16\-all"**\. SPF records are not recommended\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

**SRV — Service locator**  
An SRV record\. SRV records are used for accessing services, such as a service for email or communications\. For information about SRV record format, refer to the documentation for the service that you want to connect to\. Trailing dot is treated as optional\.  
The format of an SRV record is:  
**\[priority\] \[weight\] \[port\] \[server host name\]**  
For example:  
**1 10 5269 xmpp\-server\.example\.com\.**

**TXT — Text**  
A text record\. Enclose text in quotation marks, for example, **"Sample text entry"**\. 

## TTL \(seconds\)<a name="rrsets-values-common-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you reduce the number of calls that DNS recursive resolvers must make to Route 53 to get the latest information in this record\. This has the effect of reducing latency and reducing your bill for Route 53 service\. For more information, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\.

However, if you specify a longer value for TTL, it takes longer for changes to the record \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods before they ask Route 53 for the latest information\. If you're changing settings for a domain or subdomain that's already in use, we recommend that you initially specify a shorter value, such as 300 seconds, and increase the value after you confirm that the new settings are correct\.

If you're associating this record with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\.