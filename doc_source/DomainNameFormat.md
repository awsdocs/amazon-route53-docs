# DNS domain name format<a name="DomainNameFormat"></a>

Domain names \(including the names of domains, hosted zones, and records\) consist of a series of labels separated by dots\. Each label can be up to 63 bytes long\. The total length of a domain name cannot exceed 255 bytes, including the dots\. Amazon Route 53 supports any valid domain name\. 

Naming requirements depend on whether you're registering a domain name or you're specifying the name of a hosted zone or a record\. See the applicable topic\.

**Topics**
+ [Formatting domain names for domain name registration](#domain-name-format-registration)
+ [Formatting domain names for hosted zones and records](#domain-name-format-hosted-zones)
+ [Using an asterisk \(\*\) in the names of hosted zones and records](#domain-name-format-asterisk)
+ [Formatting internationalized domain names](#domain-name-format-idns)

## Formatting domain names for domain name registration<a name="domain-name-format-registration"></a>

For domain name registration, a domain name can contain only the characters a\-z, 0\-9, and \- \(hyphen\)\. You can't specify a hyphen at the beginning or end of a label\.

For information about how to register an internationalized domain name \(IDN\), see [Formatting internationalized domain names](#domain-name-format-idns)\.

## Formatting domain names for hosted zones and records<a name="domain-name-format-hosted-zones"></a>

For hosted zones and records, the domain name can include any of the following printable ASCII characters \(excluding spaces\):
+ a\-z
+ 0\-9
+ \- \(hyphen\)
+ \! " \# $ % & ' \( \) \* \+ , \- / : ; < = > ? @ \[ \\ \] ^ \_ ` \{ \| \} \~ \. 

Amazon Route 53 stores alphabetic characters as lowercase letters \(a\-z\), regardless of how you specify them: as uppercase letters, lowercase letters, or the corresponding letters in escape codes\. 

If your domain name contains any of the following characters, you must specify the characters by using escape codes in the format \\*three\-digit octal code*:
+ Characters 000 to 040 octal \(0 to 32 decimal, 0x00 to 0x20 hexadecimal\)
+ Characters 177 to 377 octal \(127 to 255 decimal, 0x7F to 0xFF hexadecimal\)
+ \. \(period\), character 056 octal \(46 decimal, 0x2E hexadecimal\), when used as a character in a domain name\. When using \. as a delimiter between labels, you do not need to use an escape code\.

For example, to create a hosted zone for exämple\.com, you specify `ex\344mple.com`\.

If the domain name includes any characters other than a to z, 0 to 9, \- \(hyphen\), or \_ \(underscore\), Route 53 API actions return the characters as escape codes\. This is true whether you specify the characters as characters or as escape codes when you create the entity\. The Route 53 console displays the characters as characters, not as escape codes\.

For a list of ASCII characters the corresponding octal codes, do an internet search on "ascii table"\. 

To specify an internationalized domain name \(IDN\), convert the name to Punycode\. For more information, see [Formatting internationalized domain names](#domain-name-format-idns)\.

## Using an asterisk \(\*\) in the names of hosted zones and records<a name="domain-name-format-asterisk"></a>

You can create hosted zones and records that include \* in the name\. 

**Hosted zones**
+ You can't include an \* in the leftmost label in a domain name\. For example, \*\.example\.com is not allowed\.
+ If you include \* in other positions, DNS treats it as an \* character \(ASCII 42\), not as a wildcard\.

**Records**

DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. Note the following restrictions on using \* as a wildcard in the name of a record:
+ The \* must replace the leftmost label in a domain name, for example, \*\.example\.com or \*\.acme\.example\.com\. If you include \* in any other position, such as prod\.\*\.example\.com, DNS treats it as an \* character \(ASCII 42\), not as a wildcard\.
+ The \* must replace the entire label\. For example, you can't specify \*prod\.example\.com or prod\*\.example\.com\.
+ Specific domain names take precedence\. For example, if you create records for \*\.example\.com and acme\.example\.com, Route 53 always responds to DNS queries for acme\.example\.com with the values in the acme\.example\.com record\.
+ The \* applies to DNS queries for the subdomain level that includes the asterisk, and all the subdomains of that subdomain\. For example, if you create a record named \*\.example\.com, Route 53 uses the values in that record to respond to DNS queries for zenith\.example\.com, acme\.zenith\.example\.com, and pinnacle\.acme\.zenith\.example\.com \(if there are no records that have those names\)\. 

  If you create a record named \*\.example\.com and there's no example\.com record, Route 53 responds to DNS queries for example\.com with `NXDOMAIN` \(non\-existent domain\)\.
+ You can configure Route 53 to return the same response to DNS queries both for all subdomains at the same level and for the domain name\. For example, you can configure Route 53 to respond to DNS queries such as acme\.example\.com and zenith\.example\.com using the example\.com record\. Perform the following steps:

  1. Create a record for the domain, such as example\.com\.

  1. Create an alias record for the subdomain, such as \*\.example\.com\. Specify the record that you created in step 1 as the target for the alias record\.
+ You can't use the \* as a wildcard for records that have a type of NS\.

## Formatting internationalized domain names<a name="domain-name-format-idns"></a>

When you register a new domain name or create hosted zones and records, you can specify letters other than a\-z \(for example, the ç in French\), characters in other alphabets \(for example, Cyrillic or Arabic\), and characters in Chinese, Japanese, or Korean\. Amazon Route 53 stores these internationalized domain names \(IDNs\) in Punycode, which represents Unicode characters as ASCII strings\.

If you're registering a domain name, note the following:
+ You can use characters other than a\-z, 0\-9, and \- \(hyphen\) only if the top\-level domain \(TLD\) supports IDNs and supports the language that you want to use\. To determine which languages a TLD supports, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.
+ You can specify a name in an unsupported language if the name contains only the letters a\-z\. For example, if a TLD doesn't support French but the name that you want to use includes only the characters a\-z without diacritical marks, you can still use that name\. In this example, a name that includes a "c" is allowed; a name that contains a "ç" is not\.
+ If a TLD doesn't support IDNs or doesn't support the language that you want to use for your domain name, you also can't specify the name in Punycode even though the Punycode includes only a\-z, 0\-9, and \-\.

The following example shows the Punycode representation of the internationalized domain name 中国\.asia:

`xn--fiqs8s.asia`

When you enter an IDN in the address bar of a modern browser, the browser converts it to Punycode before submitting a DNS query or making an HTTP request\.

How you enter an IDN depends on what you're creating \(domain names, hosted zones, or records\), and how you're creating it \(API, SDK, or Route 53 console\):
+ If you're using the Route 53 API or one of the AWS SDKs, you can programmatically convert a Unicode value to Punycode\. For example, if you're using Java, you can convert a Unicode value to Punycode by using the **toASCII** method of the java\.net\.IDN library\.
+ If you're using the Route 53 console to register a domain name, you can paste the name, including Unicode characters, into the name field, and the console converts the value to Punycode before saving it\.
+ If you're using the Route 53 console to create hosted zones or records, you need to convert the domain name to Punycode before you enter the name in the applicable **Name** field\. For information about online converters, perform an internet search on "punycode converter"\.

If you're registering a domain name, note that not all top\-level domains \(TLDs\) support IDNs\. For a list of TLDs supported by Route 53, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\. TLDs that don't support IDNs are noted\. 