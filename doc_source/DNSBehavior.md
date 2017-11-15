# DNS Constraints and Behaviors<a name="DNSBehavior"></a>

DNS messaging is subject to factors that affect how you create and use hosted zones and resource record sets\. This section explains these factors\.

## Maximum Response Size<a name="MaxSize"></a>

To comply with DNS standards, responses sent over UDP are limited to 512 bytes in size\. Responses exceeding 512 bytes are truncated and the resolver must re\-issue the request over TCP\. If the resolver supports EDNS0 \(as defined in [RFC 2671](http://www.linuxdig.com/rfc/individual/2671.php)\), and advertises the EDNS0 option to Amazon Route 53, Amazon Route 53 permits responses up to 4096 bytes over UDP, without truncation\.

## Authoritative Section Processing<a name="AuthSectionProcessing"></a>

For successful queries, Amazon Route 53 appends name server \(NS\) resource record sets for the relevant hosted zone to the Authority section of the DNS response\. For names that are not found \(NXDOMAIN responses\), Amazon Route 53 appends the start of authority \(SOA\) resource record set \(as defined in [RFC 1035](http://www.linuxdig.com/rfc/individual/1035.php)\) for the relevant hosted zone to the Authority section of the DNS response\.

## Additional Section Processing<a name="SectionProcessing"></a>

Amazon Route 53 appends resource record sets to the Additional section\. If the records are known and appropriate, the service appends A or AAAA resource record sets for any target of an MX, CNAME, NS, or SRV record cited in the Answer section\. For more information about these DNS record types, see [Supported DNS Record Types](ResourceRecordTypes.md)\.