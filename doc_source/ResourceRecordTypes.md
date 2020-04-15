# Supported DNS record types<a name="ResourceRecordTypes"></a>

Amazon Route 53 supports the DNS record types that are listed in this section\. Each record type also includes an example of how to format the `Value` element when you are accessing Route 53 using the API\.

**Note**  
For record types that include a domain name, enter a fully qualified domain name, for example, *www\.example\.com*\. The trailing dot is optional; Route 53 assumes that the domain name is fully qualified\. This means that Route 53 treats *www\.example\.com* \(without a trailing dot\) and *www\.example\.com\.* \(with a trailing dot\) as identical\.

Route 53 provides an extension to DNS functionality known as alias records\. Similar to CNAME records, alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets\. For more information, including a comparison of alias and CNAME records, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**Topics**
+ [A record type](#AFormat)
+ [AAAA record type](#AAAAFormat)
+ [CAA record type](#CAAFormat)
+ [CNAME record type](#CNAMEFormat)
+ [MX record type](#MXFormat)
+ [NAPTR record type](#NAPTRFormat)
+ [NS record type](#NSFormat)
+ [PTR record type](#PTRFormat)
+ [SOA record type](#SOAFormat)
+ [SPF record type](#SPFFormat)
+ [SRV record type](#SRVFormat)
+ [TXT record type](#TXTFormat)

## A record type<a name="AFormat"></a>

You use an A record to route traffic to a resource, such as a web server, using an IPv4 address in dotted decimal notation\.

**Example for the Amazon Route 53 console**

```
1. 192.0.2.1
```

**Example for the Route 53 API**

```
1. <Value>192.0.2.1</Value>
```

## AAAA record type<a name="AAAAFormat"></a>

You use an AAAA record to route traffic to a resource, such as a web server, using an IPv6 address in colon\-separated hexadecimal format\.

**Example for the Amazon Route 53 console**

```
1. 2001:0db8:85a3:0:0:8a2e:0370:7334
```

**Example for the Route 53 API**

```
1. <Value>2001:0db8:85a3:0:0:8a2e:0370:7334</Value>
```

## CAA record type<a name="CAAFormat"></a>

A CAA record specifies which certificate authorities \(CAs\) are allowed to issue certificates for a domain or subdomain\. Creating a CAA record helps to prevent the wrong CAs from issuing certificates for your domains\. A CAA record isn't a substitute for the security requirements that are specified by your certificate authority, such as the requirement to validate that you're the owner of a domain\.

You can use CAA records to specify the following:
+ Which certificate authorities \(CAs\) can issue SSL/TLS certificates, if any
+ The email address or URL to contact when a CA issues a certificate for the domain or subdomain

When you add a CAA record to your hosted zone, you specify three settings separated by spaces:

`flags tag "value"`

Note the following about the format for CAA records:
+ The value of `tag` can contain only the characters A\-Z, a\-z, and 0\-9\.
+ Always enclose `value` in quotation marks \(""\)\.
+ Some CAs allow or require additional values for `value`\. Specify additional values as name\-value pairs, and separate them with semicolons \(;\), for example:

  `0 issue "ca.example.net; account=123456"`
+ If a CA receives a request for a certificate for a subdomain \(such as www\.example\.com\) and if no CAA record for the subdomain exists, the CA submits a DNS query for a CAA record for the parent domain \(such as example\.com\)\. If a record for the parent domain exists and if the certificate request is valid, the CA issues the certificate for the subdomain\.
+ We recommend that you consult with your CA to determine what values to specify for a CAA record\.
+ You can't create a CAA record and a CNAME record that have the same name because DNS doesn't allow using the same name for both a CNAME record and any other type of record\.

**Topics**
+ [Authorize a CA to issue a certificate for a domain or subdomain](#CAAFormat-issue)
+ [Authorize a CA to issue a wildcard certificate for a domain or subdomain](#CAAFormat-issue-wild)
+ [Prevent any CA from issuing a certificate for a domain or subdomain](#CAAFormat-prevent-issue)
+ [Request that any CA contacts you if the CA receives an invalid certificate request](#CAAFormat-contact)
+ [Use another setting that is supported by the CA](#CAAFormat-custom-setting)
+ [Examples](#CAAFormat-examples)

### Authorize a CA to issue a certificate for a domain or subdomain<a name="CAAFormat-issue"></a>

To authorize a CA to issue a certificate for a domain or subdomain, create a record that has the same name as the domain or subdomain, and specify the following settings:
+ **flags** – `0`
+ **tag** – `issue`
+ **value** – the code for the CA that you authorize to issue a certificate for the domain or subdomain

For example, suppose you want to authorize ca\.example\.net to issue a certificate for example\.com\. You create a CAA record for example\.com with the following settings:

```
0 issue "ca.example.net"
```

For information about how to authorize AWS Certificate Manager to issue a certificate, see [Configure a CAA record](https://docs.aws.amazon.com/acm/latest/userguide/setup-caa.html) in the *AWS Certificate Manager User Guide*\.

### Authorize a CA to issue a wildcard certificate for a domain or subdomain<a name="CAAFormat-issue-wild"></a>

To authorize a CA to issue a wildcard certificate for a domain or subdomain, create a record that has the same name as the domain or subdomain, and specify the following settings\. A wildcard certificate applies to the domain or subdomain and all of its subdomains\.
+ **flags** – `0`
+ **tag** – `issuewild`
+ **value** – the code for the CA that you authorize to issue a certificate for a domain or subdomain, and its subdomains

For example, suppose you want to authorize ca\.example\.net to issue a wildcard certificate for example\.com, which applies to example\.com and all of its subdomains\. You create a CAA record for example\.com with the following settings:

```
0 issuewild "ca.example.net"
```

When you want to authorize a CA to issue a wildcard certificate for a domain or subdomain, create a record that has the same name as the domain or subdomain, and specify the following settings\. A wildcard certificate applies to the domain or subdomain and all of its subdomains\.

### Prevent any CA from issuing a certificate for a domain or subdomain<a name="CAAFormat-prevent-issue"></a>

To prevent any CA from issuing a certificate for a domain or subdomain, create a record that has the same name as the domain or subdomain, and specify the following settings:
+ **flags** – `0`
+ **tag** – `issue`
+ **value** – `";"`

For example, suppose you don't want any CA to issue a certificate for example\.com\. You create a CAA record for example\.com with the following settings:

`0 issue ";"`

If you don't want any CA to issue a certificate for example\.com or its subdomains, you create a CAA record for example\.com with the following settings: 

`0 issuewild ";"`

**Note**  
If you create a CAA record for example\.com and specify both of the following values, a CA that is using the value ca\.example\.net can issue the certificate for example\.com:  

```
0 issue ";"
0 issue "ca.example.net"
```

### Request that any CA contacts you if the CA receives an invalid certificate request<a name="CAAFormat-contact"></a>

If you want any CA that receives an invalid request for a certificate to contact you, specify the following settings:
+ **flags** – `0`
+ **tag** – `iodef`
+ **value** – the URL or email address that you want the CA to notify if the CA receives an invalid request for a certificate\. Use the applicable format:

  `"mailto:email-address"`

  `"http://URL"`

  `"https://URL"`

For example, if you want any CA that receives an invalid request for a certificate to send email to admin@example\.com, you create a CAA record with the following settings:

```
0 iodef "mailto:admin@example.com"
```

### Use another setting that is supported by the CA<a name="CAAFormat-custom-setting"></a>

If your CA supports a feature that isn't defined in the RFC for CAA records, specify the following settings:
+ **flags** – 128 \(This value prevents the CA from issuing a certificate if the CA doesn't support the specified feature\.\)
+ **tag** – the tag that you authorize the CA to use
+ **value** – the value that corresponds with the value of tag

For example, suppose your CA supports sending a text message if the CA receives an invalid certificate request\. \(We aren't aware of any CAs that support this option\.\) Settings for the record might be the following:

```
128 exampletag "15555551212"
```

### Examples<a name="CAAFormat-examples"></a>

**Example for the Route 53 console**

```
0 issue "ca.example.net"
0 iodef "mailto:admin@example.com"
```

**Example for the Route 53 API**

```
<ResourceRecord>
   <Value>0 issue "ca.example.net"</Value>
   <Value>0 iodef "mailto:admin@example.com"</Value>
</ResourceRecord>
```

## CNAME record type<a name="CNAMEFormat"></a>

A CNAME record maps DNS queries for the name of the current record, such as acme\.example\.com, to another domain \(example\.com or example\.net\) or subdomain \(acme\.example\.com or zenith\.example\.org\)\. 

**Important**  
The DNS protocol does not allow you to create a CNAME record for the top node of a DNS namespace, also known as the zone apex\. For example, if you register the DNS name example\.com, the zone apex is example\.com\. You cannot create a CNAME record for example\.com, but you can create CNAME records for www\.example\.com, newproduct\.example\.com, and so on\.  
In addition, if you create a CNAME record for a subdomain, you cannot create any other records for that subdomain\. For example, if you create a CNAME for www\.example\.com, you cannot create any other records for which the value of the **Name** field is www\.example\.com\.

Amazon Route 53 also supports alias records, which allow you to route queries to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets\. Aliases are similar in some ways to the CNAME record type; however, you can create an alias for the zone apex\. For more information, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**Example for the Route 53 console**

```
1. hostname.example.com
```

**Example for the Route 53 API**

```
1. <Value>hostname.example.com</Value>
```

## MX record type<a name="MXFormat"></a>

An MX record specifies the names of your mail servers and, if you have two or more mail servers, the priority order\. Each value for an MX record contains two values, priority and domain name:

**Priority**  
An integer that represents the priority for an email server\. If you specify only one server, the priority can be any integer between 0 and 65535\. If you specify multiple servers, the value that you specify for the priority indicates which email server you want email to be routed to first, second, and so on\. The server with the lowest value for the priority takes precedence\. For example, if you have two email servers and you specify values of 10 and 20 for the priority, email always goes to the server with a priority of 10 unless it's unavailable\. If you specify values of 10 and 10, email is routed to the two servers approximately equally\.

**Domain name**  
The domain name of the email server\. Specify the name \(such as mail\.example\.com\) of an A or AAAA record\. In [RFC 2181, Clarifications to the DNS Specification](https://tools.ietf.org/html/rfc2181), section 10\.3 forbids specifying the name of a CNAME record for the domain name value\. \(When the RFC mentions "alias," it means a CNAME record, not a Route 53 alias record\.\)

**Example for the Amazon Route 53 console**

```
1. 10 mail.example.com
```

**Example for the Route 53 API**

```
1. <Value>10 mail.example.com</Value>
```

## NAPTR record type<a name="NAPTRFormat"></a>

A Name Authority Pointer \(NAPTR\) is a type of record that is used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For example, one common use is to convert phone numbers into SIP URIs\. 

The `Value` element for an NAPTR record consists of six space\-separated values:

**Order**  
When you specify more than one record, the sequence that you want the DDDS application to evaluate records in\. Valid values: 0\-65535\.

**Preference**  
When you specify two or more records that have the same **Order**, your preference for the sequence that those records are evaluated in\. For example, if two records have an **Order** of 1, the DDDS application first evaluates the record that has the lower **Preference**\. Valid values: 0\-65535\.

**Flags**  
A setting that is specific to DDDS applications\. Values currently defined in [RFC 3404](https://www.ietf.org/rfc/rfc3404.txt) are uppercase\- and lowercase letters **"A"**, **"P"**, **"S"**, and **"U"**, and the empty string, **""**\. Enclose **Flags** in quotation marks\. 

**Service**  
A setting that is specific to DDDS applications\. Enclose **Service** in quotation marks\.  
For more information, see the applicable RFCs:  
+ **URI DDDS application** – [https://tools\.ietf\.org/html/rfc3404\#section\-4\.4](https://tools.ietf.org/html/rfc3404#section-4.4)
+ **S\-NAPTR DDDS application** – [https://tools\.ietf\.org/html/rfc3958\#section\-6\.5](https://tools.ietf.org/html/rfc3958#section-6.5)
+ **U\-NAPTR DDDS application** – [https://tools\.ietf\.org/html/rfc4848\#section\-4\.5](https://tools.ietf.org/html/rfc4848#section-4.5)

**Regexp**  
A regular expression that the DDDS application uses to convert an input value into an output value\. For example, an IP phone system might use a regular expression to convert a phone number that is entered by a user into a SIP URI\. Enclose **Regexp** in quotation marks\. Specify either a value for **Regexp** or a value for **Replacement**, but not both\.  
The regular expression can include any of the following printable ASCII characters:  
+ a\-z
+ 0\-9
+ \- \(hyphen\)
+ \(space\)
+ \! \# $ % & ' \( \) \* \+ , \- / : ; < = > ? @ \[ \] ^ \_ ` \{ \| \} \~ \.
+ " \(quotation mark\)\. To include a literal quote in a string, precede it with a \\ character: \\"\.
+ \\ \(backslash\)\. To include a backslash in a string, precede it with a \\ character: \\\\\.
Specify all other values, such as internationalized domain names, in octal format\.  
For the syntax for **Regexp**, see [RFC 3402, section 3\.2, Substitution Expression Syntax](https://tools.ietf.org/html/rfc3402#section-3.2)

**Replacement**  
The fully qualified domain name \(FQDN\) of the next domain name that you want the DDDS application to submit a DNS query for\. The DDDS application replaces the input value with the value that you specify for **Replacement**, if any\. Specify either a value for **Regexp** or a value for **Replacement**, but not both\. If you specify a value for **Regexp**, specify a dot \(**\.**\) for **Replacement**\.  
The domain name can include a\-z, 0\-9, and \- \(hyphen\)\.

For more information about DDDS applications and about NAPTR records, see the following RFCs:
+ [RFC 3401](https://www.ietf.org/rfc/rfc3401.txt)
+ [RFC 3402](https://www.ietf.org/rfc/rfc3402.txt)
+ [RFC 3403](https://www.ietf.org/rfc/rfc3403.txt)
+ [RFC 3404](https://www.ietf.org/rfc/rfc3404.txt)

**Example for the Amazon Route 53 console**

```
1. 100 50 "u" "E2U+sip" "!^(\\+441632960083)$!sip:\\1@example.com!" .
2. 100 51 "u" "E2U+h323" "!^\\+441632960083$!h323:operator@example.com!" .
3. 100 52 "u" "E2U+email:mailto" "!^.*$!mailto:info@example.com!" .
```

**Example for the Route 53 API**

```
1. <ResourceRecord>
2.    <Value>100 50 "u" "E2U+sip" "!^(\\+441632960083)$!sip:\\1@example.com!" .</Value>
3.    <Value>100 51 "u" "E2U+h323" "!^\\+441632960083$!h323:operator@example.com!" .</Value>
4.    <Value>100 52 "u" "E2U+email:mailto" "!^.*$!mailto:info@example.com!" .</Value>
5. </ResourceRecord>
```

## NS record type<a name="NSFormat"></a>

An NS record identifies the name servers for the hosted zone\. Note the following:
+ The most common use for an NS record is to control how internet traffic is routed for a domain\. To use the records in a hosted zone to route traffic for a domain, you update the domain registration settings to use the four name servers in the default NS record\. \(This is the NS record that has the same name as the hosted zone\.\)
+ You can create a separate hosted zone for a subdomain \(acme\.example\.com\) and use that hosted zone to route internet traffic for the subdomain and its subdomains \(subdomain\.acme\.example\.com\)\. You set up this configuration, known as "delegating responsibility for a subdomain to a hosted zone" by creating another NS record in the hosted zone for the root domain \(example\.com\)\. For more information, see [Routing traffic for subdomains](dns-routing-traffic-for-subdomains.md)\.
+ You also use NS records to configure white\-label name servers\. For more information, see [Configuring white\-label name servers](white-label-name-servers.md)\.

For more information about NS records, see [NS and SOA records that Amazon Route 53 creates for a public hosted zone](SOA-NSrecords.md)\.

**Example for the Amazon Route 53 console**

```
1. ns-1.example.com
```

**Example for the Route 53 API**

```
1. <Value>ns-1.example.com</Value>
```

## PTR record type<a name="PTRFormat"></a>

A PTR record maps an IP address to the corresponding domain name\.

**Example for the Amazon Route 53 console**

```
1. hostname.example.com
```

**Example for the Route 53 API**

```
1. <Value>hostname.example.com</Value>
```

## SOA record type<a name="SOAFormat"></a>

A start of authority \(SOA\) record provides information about a domain and the corresponding Amazon Route 53 hosted zone\. For information about the fields in an SOA record, see [NS and SOA records that Amazon Route 53 creates for a public hosted zone](SOA-NSrecords.md)\.

**Example for the Route 53 console**

```
1. ns-2048.awsdns-64.net hostmaster.awsdns.com 1 1 1 1 60
```

**Example for the Route 53 API**

```
1. <Value>ns-2048.awsdns-64.net hostmaster.awsdns.com 1 1 1 1 60</Value>
```

## SPF record type<a name="SPFFormat"></a>

SPF records were formerly used to verify the identity of the sender of email messages\. However, we no longer recommend that you create records for which the record type is SPF\. RFC 7208, *Sender Policy Framework \(SPF\) for Authorizing Use of Domains in Email, Version 1*, has been updated to say, "\.\.\.\[I\]ts existence and mechanism defined in \[RFC4408\] have led to some interoperability issues\. Accordingly, its use is no longer appropriate for SPF version 1; implementations are not to use it\." In RFC 7208, see section 14\.1, [The SPF DNS Record Type](http://tools.ietf.org/html/rfc7208#section-14.1)\.

Instead of an SPF record, we recommend that you create a TXT record that contains the applicable value\. For more information about valid values, see the Wikipedia article [Sender Policy Framework](https://en.wikipedia.org/wiki/Sender_Policy_Framework)\.

**Example for the Amazon Route 53 console**

```
1. "v=spf1 ip4:192.168.0.1/16 -all"
```

**Example for the Route 53 API**

```
1. <Value>"v=spf1 ip4:192.168.0.1/16 -all"</Value>
```

## SRV record type<a name="SRVFormat"></a>

An SRV record `Value` element consists of four space\-separated values\. The first three values are decimal numbers representing priority, weight, and port\. The fourth value is a domain name\. For information about SRV record format, refer to the applicable documentation\.

**Example for the Amazon Route 53 console**

```
1. 10 5 80 hostname.example.com
```

**Example for the Route 53 API**

```
1. <Value>10 5 80 hostname.example.com</Value>
```

## TXT record type<a name="TXTFormat"></a>

A TXT record contains one or more strings that are enclosed in double quotation marks \(`"`\)\. When you use the simple [routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html), include all values for a domain \(example\.com\) or subdomain \(www\.example\.com\) in the same TXT record\.

**Topics**
+ [Entering TXT record values](#TXTformat-limits)
+ [Special characters in a TXT record value](#TXTformat-special-characters)
+ [Uppercase and lowercase in a TXT record value](#TXTformat-case)
+ [Examples](#TXTformat-examples)

### Entering TXT record values<a name="TXTformat-limits"></a>

A single string can include up to 255 characters, including the following:
+ a\-z
+ A\-Z
+ 0\-9
+ Space
+ \- \(hyphen\)
+ \! " \# $ % & ' \( \) \* \+ , \- / : ; < = > ? @ \[ \\ \] ^ \_ ` \{ \| \} \~ \. 

If you need to enter a value longer than 255 characters, break the value into strings of 255 characters or fewer, and enclose each string in double quotation marks \(`"`\)\. In the console, list all the strings on the same line:

```
1. "String 1" "String 2" "String 3"
```

For the API, include all the strings in the same `Value` element:

```
1. <Value>"String 1" "String 2" "String 3"</Value>
```

The maximum length of a value in a TXT record is 4,000 characters\. 

### Special characters in a TXT record value<a name="TXTformat-special-characters"></a>

If your TXT record contains any of the following characters, you must specify the characters by using escape codes in the format `\`*three\-digit octal code*:
+ Characters 000 to 040 octal \(0 to 32 decimal, 0x00 to 0x20 hexadecimal\)
+ Characters 177 to 377 octal \(127 to 255 decimal, 0x7F to 0xFF hexadecimal\)

For example, if the value of your TXT record is `"exämple.com"`, you specify `"ex\344mple.com"`\.

For a mapping between ASCII characters and octal codes, perform an internet search for "ascii octal codes\." One useful reference is [ASCII Code \- The extended ASCII table](https://www.ascii-code.com/)\. 

To include a quotation mark \(`"`\) in a string, put a backslash \(`\`\) character before the quotation mark: `\"`\. 

### Uppercase and lowercase in a TXT record value<a name="TXTformat-case"></a>

Case is preserved, so `"Ab"` and `"aB"` are different values\.

### Examples<a name="TXTformat-examples"></a>

**Example for the Amazon Route 53 console**

Put each value on a separate line:

```
1. "This string includes \"quotation marks\"."
2. "The last character in this string is an accented e specified in octal format: \351"
3. "v=spf1 ip4:192.168.0.1/16 -all"
```

**Example for the Route 53 API**

Put each value in a separate `Value` element:

```
1. <Value>"This string includes \"quotation marks\"."</Value>
2. <Value>"The last character in this string is an accented e specified in octal format: \351"</Value>
3. <Value>"v=spf1 ip4:192.168.0.1/16 -all"</Value>
```