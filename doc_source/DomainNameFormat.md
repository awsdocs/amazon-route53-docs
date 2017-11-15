# DNS Domain Name Format<a name="DomainNameFormat"></a>

Domain names \(including the names of domains, hosted zones, and resource record sets\) consist of a series of labels separated by dots\. Each label can be up to 63 bytes long\. The total length of a domain name cannot exceed 255 bytes, including the dots\. Amazon Route 53 supports any valid domain name\. 

Naming requirements depend on whether you're registering a domain name or you're specifying the name of a hosted zone or a resource record set\. See the applicable topic\.


+ [Formatting Domain Names for Domain Name Registration](#domain-name-format-registration)
+ [Formatting Domain Names for Hosted Zones and Resource Record Sets](#domain-name-format-hosted-zones)
+ [Using an Asterisk \(\*\) in the Names of Hosted Zones and Resource Record Sets](#domain-name-format-asterisk)
+ [Formatting Internationalized Domain Names](#domain-name-format-idns)

## Formatting Domain Names for Domain Name Registration<a name="domain-name-format-registration"></a>

For domain name registration, a domain name can contain only the characters a\-z, 0\-9, and – \(hyphen\)\. You can't specify a hyphen at the beginning or end of a label\.

For information about how to register an internationalized domain name \(IDN\), see [Formatting Internationalized Domain Names](#domain-name-format-idns)\.

## Formatting Domain Names for Hosted Zones and Resource Record Sets<a name="domain-name-format-hosted-zones"></a>

For hosted zones and resource record sets, the domain name can include any of the following printable ASCII characters \(excluding spaces\):

+ a\-z

+ 0\-9

+ \- \(hyphen\)

+ \! " \# $ % & ' \( \) \* \+ , \- / : ; < = > ? @ \[ \\ \] ^ \_ ` \{ | \} \~ \. 

Amazon Route 53 stores alphabetic characters as lowercase letters \(a\-z\), regardless of how you specify them: as uppercase letters, lowercase letters, or the corresponding letters in escape codes\. 

If your domain name contains any of the following characters, you must specify the characters by using escape codes in the format \\*three\-digit octal code*:

+ Characters 000 to 040 octal \(0 to 32 decimal, 0x00 to 0x20 hexadecimal\)

+ Characters 177 to 377 octal \(127 to 255 decimal, 0x7F to 0xFF hexadecimal\)

+ \. \(period\), character 056 octal \(46 decimal, 0x2E hexadecimal\), when used as a character in a domain name\. When using \. as a delimiter between labels, you do not need to use an escape code\.

For example, to create a hosted zone for exämple\.com, you specify `ex\344mple.com`\.

If the domain name includes any characters other than a to z, 0 to 9, \- \(hyphen\), or \_ \(underscore\), Amazon Route 53 API actions return the characters as escape codes\. This is true whether you specify the characters as characters or as escape codes when you create the entity\. The Amazon Route 53 console displays the characters as characters, not as escape codes\.

For a list of ASCII characters the corresponding octal codes, do an internet search on "ascii table"\. 

To specify an internationalized domain name \(IDN\), convert the name to Punycode\. For more information, see [Formatting Internationalized Domain Names](#domain-name-format-idns)\.

## Using an Asterisk \(\*\) in the Names of Hosted Zones and Resource Record Sets<a name="domain-name-format-asterisk"></a>

You can create hosted zones that include \* in the name\. Note the following:

+ You can't include an \* in the leftmost label in a domain name\. For example, \*\.example\.com is not allowed\.

+ If you include \* in other positions, DNS treats it as an \* character \(ASCII 42\), not as a wildcard\.

You can also create resource record sets that include \* in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. Note the following restrictions on using \* as a wildcard in the name of resource record sets:

+ The \* must replace the leftmost label in a domain name, for example, \*\.example\.com\. It can't replace any of the middle labels, for example, marketing\.\*\.example\.com\.

+ The \* must replace the entire label\. For example, you can't specify \*prod\.example\.com or prod\*\.example\.com\.

+ You can't use the \* as a wildcard for resource records sets that have a type of NS\.

For resource record sets, if you include \* in any position other than the leftmost label in a domain name, DNS treats it as an \* character \(ASCII 42\), not as a wildcard\.

## Formatting Internationalized Domain Names<a name="domain-name-format-idns"></a>

When you register a new domain name or create hosted zones and resource record sets, you can specify characters in other alphabets \(for example, Cyrillic or Arabic\) and characters in Chinese, Japanese, or Korean\. Amazon Route 53 stores these internationalized domain names \(IDNs\) in Punycode, which represents Unicode characters as ASCII strings\.

The following example shows the Punycode representation of the internationalized domain name ![\[China\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/china.png)\.asia:

`xn--fiqs8s.asia`

When you enter an IDN in the address bar of a modern browser, the browser converts it to Punycode before submitting a DNS query or making an HTTP request\.

How you enter an IDN depends on what you're creating \(domain names, hosted zones, or resource record sets\), and how you're creating it \(API, SDK, or Amazon Route 53 console\):

+ If you're using the Amazon Route 53 API or one of the AWS SDKs, you can programmatically convert a Unicode value to Punycode\. For example, if you're using Java, you can convert a Unicode value to Punycode by using the **toASCII** method of the java\.net\.IDN library\.

+ If you're using the Amazon Route 53 console to register a domain name, you can paste the name, including Unicode characters, into the name field, and the console converts the value to Punycode before saving it\.

+ If you're using the Amazon Route 53 console to create hosted zones or resource record sets, you need to convert the domain name to Punycode before you enter the name in the applicable **Name** field\. For information about online converters, perform an internet search on "punycode converter"\.

If you're registering a domain name, note that not all top\-level domains \(TLDs\) support IDNs\. For a list of TLDs supported by Amazon Route 53, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\. TLDs that don't support IDNs are noted\. 