# DNS constraints and behaviors<a name="DNSBehavior"></a>

DNS messaging is subject to factors that affect how you create and use hosted zones and records\. This section explains these factors\.

## Maximum response size<a name="MaxSize"></a>

To comply with DNS standards, responses sent over UDP are no more than 512 bytes in size\. Responses exceeding 512 bytes are truncated and the resolver must re\-issue the request over TCP\. If the resolver supports EDNS0 \(as defined in [RFC 2671](https://tools.ietf.org/html/rfc2671)\), and advertises the EDNS0 option to Amazon Route 53, Route 53 permits responses up to 4096 bytes over UDP, without truncation\.

## Authoritative section processing<a name="AuthSectionProcessing"></a>

For successful queries, Route 53 appends name server \(NS\) records for the relevant hosted zone to the Authority section of the DNS response\. For names that are not found \(NXDOMAIN responses\), Route 53 appends the start of authority \(SOA\) record \(as defined in [RFC 1035](https://tools.ietf.org/html/rfc1035)\) for the relevant hosted zone to the Authority section of the DNS response\.

## Additional section processing<a name="SectionProcessing"></a>

Route 53 appends records to the Additional section\. If the records are known and appropriate, the service appends A or AAAA records for any target of an MX, CNAME, NS, or SRV record cited in the Answer section\. For more information about these DNS record types, see [Supported DNS record types](ResourceRecordTypes.md)\.