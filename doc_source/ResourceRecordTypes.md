# Supported DNS Record Types<a name="ResourceRecordTypes"></a>

Amazon Route 53 supports the DNS resource record types that are listed in this section\. Each record type also includes an example of how to format the `Value` element when you are accessing Amazon Route 53 using the API\.

**Note**  
For resource record types that include a domain name, enter a fully qualified domain name, for example, *www\.example\.com*\. The trailing dot is optional; Amazon Route 53 assumes that the domain name is fully qualified\. This means that Amazon Route 53 treats *www\.example\.com* \(without a trailing dot\) and *www\.example\.com\.* \(with a trailing dot\) as identical\.


+ [A Format](#AFormat)
+ [AAAA Format](#AAAAFormat)
+ [CAA Format](#CAAFormat)
+ [CNAME Format](#CNAMEFormat)
+ [MX Format](#MXFormat)
+ [NAPTR Format](#NAPTRFormat)
+ [NS Format](#NSFormat)
+ [PTR Format](#PTRFormat)
+ [SOA Format](#SOAFormat)
+ [SPF Format](#SPFFormat)
+ [SRV Format](#SRVFormat)
+ [TXT Format](#TXTFormat)

## A Format<a name="AFormat"></a>

The value for an A record is an IPv4 address in dotted decimal notation\.

**Example for the Amazon Route 53 console**

```
1. 192.0.2.1
```

**Example for the Amazon Route 53 API**

```
1. <Value>192.0.2.1</Value>
```

## AAAA Format<a name="AAAAFormat"></a>

The value for a AAAA record is an IPv6 address in colon\-separated hexadecimal format\.

**Example for the Amazon Route 53 console**

```
1. 2001:0db8:85a3:0:0:8a2e:0370:7334
```

**Example for the Amazon Route 53 API**

```
1. <Value>2001:0db8:85a3:0:0:8a2e:0370:7334</Value>
```

## CAA Format<a name="CAAFormat"></a>

A CAA record lets you specify which certificate authorities \(CAs\) are allowed to issue certificates for a domain or subdomain\. Creating a CAA record helps to prevent the wrong CAs from issuing certificates for your domains\. A CAA record isn't a substitute for the security requirements that are specified by your certificate authority, such as the requirement to validate that you're the owner of a domain\.

You can use CAA records to specify the following:

+ Which certificate authorities \(CAs\) can issue SSL/TLS certificates, if any

+ The email address or URL to contact when a CA issues a certificate for the domain or subdomain

In both the Amazon Route 53 console and the Amazon Route 53 API, the **Value** element for a CAA record includes three space\-separated values\.

**Note**  
We recommend that you consult with your CA to determine what values to specify for a CAA record\.

**flags**  
The value of **flags** can be one of the following:  

+ **0** – Always specify **0** unless you specify a value for **tag** that is unsupported by some CAs

+ **128** – If the value of **tag** is unsupported by a CA, the CA should not issue a certificate for the domain or subdomain

**tag**  
The value of **tag** can be one of the following:    
**issue**  
Indicates that the CA specified by **value** is authorized to issue a certificate for the domain or subdomain that has the same name as the current record\.  
**issuewild**  
Indicates that the CA specified by **value** is authorized to issue a wildcard certificate for the domain or subdomain that has the same name as the current record\. A wildcard certificate applies to the domain or subdomain and all of its subdomains\.  
**iodef**  
Indicates that you want the CA to contact the URL or email address that you specify in **value** if the CA receives an invalid request for a certificate\.  
**another value**  
If the CA supports values for **tag** other than **issue**, **issuewild**, and **iodef**, the tag that you authorize the CA to use\. If the value of **flags** is **128**, the CA won't issue a certificate if the CA doesn't support the value that you specify for **tag**\.

**value**  
The value of **value** depends on the value of **tag**\. Enclose the value in quotation marks \(**""**\)\.  
Some CAs allow or require additional values for **value**\. Specify additional values as name\-value pairs, and separate them with semicolons \(**;**\), for example:  
`0 issue "ca.example.net; account=123456"`  
When **tag** is **issue**  
One of the following values:  

+ The domain of a CA that can issue a certificate for this domain or subdomain, for example, **ca\.example\.net**

+ **;** \(semicolon\), which indicates that no CA should issue a certificate for this domain or subdomain
In the following example, the CA with the domain name **ca\.example\.net** is authorized to issue a certificate for the domain or subdomain that has the same name as the current record:  
**"ca\.example\.net"**  
In the following example, no CA is allowed to issue certificates for the domain that has the same name as the current record:  
**";"**  
When **tag** is **issuewild**  
The same as when **tag** is **issue**, except that the settings apply to wildcard certificates\.  
When **tag** is **iodef**  
The URL or email address that you want the CA to notify if the CA receives an invalid request for a certificate\. Use the applicable format:  
**"mailto:*email\-address*"**  
**"http://*URL*"**  
**"https://*URL*"**  
When **tag** is another value  
Specify the applicable value that corresponds with the value of **tag**\.

**Example for the Amazon Route 53 console**

```
0 issue "ca.example.net"
0 iodef "mailto:admin@example.com"
```

**Example for the Amazon Route 53 API**

```
<ResourceRecord>
   <Value>0 issue "ca.example.net"</Value>
   <Value>0 iodef "mailto:admin@example.com"</Value>
</ResourceRecord>
```

## CNAME Format<a name="CNAMEFormat"></a>

A CNAME `Value` element is the same format as a domain name\.

**Important**  
The DNS protocol does not allow you to create a CNAME record for the top node of a DNS namespace, also known as the zone apex\. For example, if you register the DNS name example\.com, the zone apex is example\.com\. You cannot create a CNAME record for example\.com, but you can create CNAME records for www\.example\.com, newproduct\.example\.com, and so on\.  
In addition, if you create a CNAME record for a subdomain, you cannot create any other resource record sets for that subdomain\. For example, if you create a CNAME for www\.example\.com, you cannot create any other resource record sets for which the value of the Name field is www\.example\.com\.

Amazon Route 53 also supports alias resource record sets, which allow you to route queries to a CloudFront distribution, an Elastic Beanstalk environment, an ELB Classic, Application, or Network Load Balancer, an Amazon S3 bucket that is configured as a static website, or another Amazon Route 53 resource record set\. Aliases are similar in some ways to the CNAME resource record type; however, you can create an alias for the zone apex\. For more information, see [Choosing Between Alias and Non\-Alias Resource Record Sets](resource-record-sets-choosing-alias-non-alias.md)\.

**Example for the Amazon Route 53 console**

```
1. hostname.example.com
```

**Example for the Amazon Route 53 API**

```
1. <Value>hostname.example.com</Value>
```

## MX Format<a name="MXFormat"></a>

Each value for an MX resource record set actually contains two values: 

+ An integer that represents the priority for an email server

+ The domain name of the email server

If you specify only one server, the priority can be any integer between 0 and 65535\. If you specify multiple servers, the value that you specify for the priority indicates which email server you want email to be routed to first, second, and so on\. For example, if you have two email servers and you specify values of 10 and 20 for the priority, email always goes to the server with a priority of 10 unless it's unavailable\. If you specify values of 10 and 10, email is routed to the two servers approximately equally\.

**Example for the Amazon Route 53 console**

```
1. 10 mail.example.com
```

**Example for the Amazon Route 53 API**

```
1. <Value>10 mail.example.com</Value>
```

## NAPTR Format<a name="NAPTRFormat"></a>

A Name Authority Pointer \(NAPTR\) is a type of resource record set that is used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For example, one common use is to convert phone numbers into SIP URIs\. 

The `Value` element for an NAPTR resource record set consists of six space\-separated values:

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

+ \! \# $ % & ' \( \) \* \+ , \- / : ; < = > ? @ \[ \] ^ \_ ` \{ | \} \~ \.

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

**Example for the Amazon Route 53 API**

```
1. <ResourceRecord>
2.    <Value>100 50 "u" "E2U+sip" "!^(\\+441632960083)$!sip:\\1@example.com!" .</Value>
3.    <Value>100 51 "u" "E2U+h323" "!^\\+441632960083$!h323:operator@example.com!" .</Value>
4.    <Value>100 52 "u" "E2U+email:mailto" "!^.*$!mailto:info@example.com!" .</Value>
5. </ResourceRecord>
```

## NS Format<a name="NSFormat"></a>

An NS record identifies the name servers for the hosted zone\. The value for an NS record is the domain name of a name server\. For more information about NS records, see [NS and SOA Resource Record Sets that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)\. For information about configuring white label name servers, see [Configuring White Label Name Servers](white-label-name-servers.md)\.

**Example for the Amazon Route 53 console**

```
1. ns-1.example.com
```

**Example for the Amazon Route 53 API**

```
1. <Value>ns-1.example.com</Value>
```

## PTR Format<a name="PTRFormat"></a>

A PTR record `Value` element is the same format as a domain name\.

**Example for the Amazon Route 53 console**

```
1. hostname.example.com
```

**Example for the Amazon Route 53 API**

```
1. <Value>hostname.example.com</Value>
```

## SOA Format<a name="SOAFormat"></a>

A start of authority \(SOA\) record provides information about a domain and the corresponding Amazon Route 53 hosted zone\. For information about the fields in an SOA record, see [NS and SOA Resource Record Sets that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)\.

**Example for the Amazon Route 53 console**

```
1. ns-2048.awsdns-64.net hostmaster.awsdns.com 1 1 1 1 60
```

**Example for the Amazon Route 53 API**

```
1. <Value>ns-2048.awsdns-64.net hostmaster.awsdns.com 1 1 1 1 60</Value>
```

## SPF Format<a name="SPFFormat"></a>

SPF records were formerly used to verify the identity of the sender of email messages\. However, we no longer recommend that you create resource record sets for which the record type is SPF\. RFC 7208, *Sender Policy Framework \(SPF\) for Authorizing Use of Domains in Email, Version 1*, has been updated to say, "\.\.\.\[I\]ts existence and mechanism defined in \[RFC4408\] have led to some interoperability issues\. Accordingly, its use is no longer appropriate for SPF version 1; implementations are not to use it\." In RFC 7208, see section 14\.1, [The SPF DNS Record Type](http://tools.ietf.org/html/rfc7208#section-14.1)\.

Instead of an SPF record, we recommend that you create a TXT record that contains the applicable value\. For more information about valid values, see [Sender Policy Framework, SPF Record Syntax](http://www.openspf.org/SPF_Record_Syntax)\.

**Example for the Amazon Route 53 console**

```
1. "v=spf1 ip4:192.168.0.1/16 -all"
```

**Example for the Amazon Route 53 API**

```
1. <Value>"v=spf1 ip4:192.168.0.1/16 -all"</Value>
```

## SRV Format<a name="SRVFormat"></a>

An SRV record `Value` element consists of four space\-separated values\. The first three values are decimal numbers representing priority, weight, and port\. The fourth value is a domain name\. For information about SRV record format, refer to the applicable documentation\.

**Example for the Amazon Route 53 console**

```
1. 10 5 80 hostname.example.com
```

**Example for the Amazon Route 53 API**

```
1. <Value>10 5 80 hostname.example.com</Value>
```

## TXT Format<a name="TXTFormat"></a>

A TXT record contains a space\-separated list of double\-quoted strings\. A single string include a maximum of 255 characters\. In addition to the characters that are permitted unescaped in domain names, space is allowed in TXT strings\. All other octet values must be quoted in octal form\. Unlike domain names, case is preserved in character strings, meaning that `Ab` is not the same as `aB`\. You can include a literal quote in a string by preceding it with a `\` character\.

**Example for the Amazon Route 53 console**

```
1. "This string includes \"quotation marks\"." "The last character in this string is an accented e specified in octal format: \351"
```

**Example for the Amazon Route 53 API**

```
1. <Value>"This string includes \"quotation marks\"." "The last character in this string is an accented e specified in octal format: \351"</Value>
```