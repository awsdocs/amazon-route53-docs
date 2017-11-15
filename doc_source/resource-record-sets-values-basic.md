# Values for Basic Resource Record Sets<a name="resource-record-sets-values-basic"></a>

When you create basic resource record sets, you specify the following values:


+ [Name](#rrsets-values-basic-name)
+ [Type](#rrsets-values-basic-type)
+ [Alias](#rrsets-values-basic-alias)
+ [TTL \(Time to Live\)](#rrsets-values-basic-ttl)
+ [Value](#rrsets-values-basic-value)
+ [Routing Policy](#rrsets-values-basic-routing-policy)

## Name<a name="rrsets-values-basic-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a resource record set that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

**CNAME resource record sets**  
If you're creating a resource record set that has a value of **CNAME** for **Type**, the name of the resource record set can't be the same as the name of the hosted zone\.

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an Asterisk \(\*\) in the Names of Hosted Zones and Resource Record Sets](DomainNameFormat.md#domain-name-format-asterisk)\.  
You can't use the \* wildcard for resource records sets that have a type of **NS**\.

## Type<a name="rrsets-values-basic-type"></a>

The DNS record type\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

Select the value for **Type** based on how you want Amazon Route 53 to respond to DNS queries\. 

## Alias<a name="rrsets-values-basic-alias"></a>

Select **No**\. 

## TTL \(Time to Live\)<a name="rrsets-values-basic-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this resource record set\. If you specify a longer value \(for example, 172800 seconds, or two days\), you pay less for Amazon Route 53 service because recursive resolvers send requests to Amazon Route 53 less often\. However, it takes longer for changes to the resource record set \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods instead of asking Amazon Route 53 for the latest information\. 

If you're associating this resource record set with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\.

## Value<a name="rrsets-values-basic-value"></a>

Enter a value that is appropriate for the value of **Type**\. For all types except **CNAME**, you can enter more than one value\. Enter each value on a separate line\.

**A — IPv4 address**  
An IP address in IPv4 format, for example, **192\.0\.2\.235**\.

**AAAA — IPv6 address**  
An IP address in IPv6 format, for example, **2001:0db8:85a3:0:0:8a2e:0370:7334**\.

**CAA — Certificate Authority Authorization**  
Three space\-separated values that control which certificate authorities are allowed to issue certificates or wildcard certificates for the domain or subdomain that is specified by **Name**\. You can use CAA records to specify the following:  

+ Which certificate authorities \(CAs\) can issue SSL/TLS certificates, if any

+ The email address or URL to contact when a CA issues a certificate for the domain or subdomain

**CNAME — Canonical name**  
The fully qualified domain name \(for example, *www\.example\.com*\) that you want Amazon Route 53 to return in response to DNS queries for this resource record set\. A trailing dot is optional; Amazon Route 53 assumes that the domain name is fully qualified\. This means that Amazon Route 53 treats *www\.example\.com* \(without a trailing dot\) and *www\.example\.com\.* \(with a trailing dot\) as identical\.

**MX — Mail exchange**  
A priority and a domain name that specifies a mail server, for example, **10 mailserver\.example\.com**\.

**NAPTR — Name Authority Pointer**  
Six space\-separated settings that are used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For more information, see [NAPTR Format](ResourceRecordTypes.md#NAPTRFormat)\.

**NS — Name server**  
The domain name of a name server, for example, **ns1\.example\.com**\.

**PTR — Pointer**  
The domain name that you want Amazon Route 53 to return\.

**SOA — Start of Authority**  
Basic DNS information about the domain\. For more information, see [The Start of Authority \(SOA\) Resource Record Set](SOA-NSrecords.md#SOArecords)\.

**SPF — Sender Policy Framework**  
An SPF record enclosed in quotation marks, for example, **"v=spf1 ip4:192\.168\.0\.1/16\-all"**\. SPF records are not recommended\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

**SRV — Service locator**  
An SRV record\. For information about SRV record format, refer to the applicable documentation\. The format of an SRV record is:  
**\[priority\] \[weight\] \[port\] \[server host name\]**  
For example:  
**1 10 5269 xmpp\-server\.example\.com\.**

**TXT — Text**  
A text record\. Enclose text in quotation marks, for example, **"Sample Text Entry"**\. 

## Routing Policy<a name="rrsets-values-basic-routing-policy"></a>

Select **Simple**\.