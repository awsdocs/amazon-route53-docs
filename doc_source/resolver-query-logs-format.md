# Values that appear in Resolver query logs<a name="resolver-query-logs-format"></a>

Each log file contains one log entry for each DNS query that Amazon Route 53 received from DNS resolvers in the corresponding edge location\. Each log entry includes the following values:

**version**  
The version number of the query log format\. If we add fields to the log or change the format of existing fields, we'll increment this value\.

**account\_id**  
The ID of the AWS account that created the VPC\.

**region**  
The AWS Region that you created the VPC in\.

**vpc\_id**  
The ID of the VPC that the query originated in\.

**query\_timestamp**  
The date and time that the query was submitted, in ISO 8601 format and Coordinated Universal Time \(UTC\), for example, `2017-03-16T19:20:25.177Z`\.   
For information about ISO 8601 format, see the Wikipedia article [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)\. For information about UTC, see the Wikipedia article [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)\.

**query\_name**  
The domain name \(example\.com\) or subdomain name \(www\.example\.com\) that was specified in the query\.

**query\_type**  
Either the DNS record type that was specified in the request, or `ANY`\. For information about the types that Route 53 supports, see [Supported DNS record types](ResourceRecordTypes.md)\.

**query\_class**  
The class of the query\.

**rcode**  
The DNS response code that Resolver returned in response to the DNS query\. The response code indicates whether the query was valid or not\. The most common response code is `NOERROR`, meaning that the query was valid\. If the response is not valid, Resolver returns a response code that explains why not\. For a list of possible response codes, see [DNS RCODEs](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6) on the IANA website\.

**answer\_type**  
The DNS record type \(such as A, MX, or CNAME\) of the value that Resolver is returning in response to the query\. For information about the types that Route 53 supports, see [Supported DNS record types](ResourceRecordTypes.md)\.

**rdata**  
The value that Resolver returned in response to the query\. For example, for an A record, this is an IP address in IPv4 format\. For a CNAME record, this is the domain name in the CNAME record\. 

**answer\_class**  
The class of the Resolver response to the query\.

**srcaddr**  
The IP address of the instance that the query originated from\.

**srcport**  
The port on the instance that the query originated from\.

**transport**  
The protocol used to submit the DNS query\.

**srcids**  
The list of IDs of the sources the DNS query originated from or passed through\.

**instance**  
The ID of the instance that the query originated from\.

**resolver\-endpoint**  
The ID of the resolver endpoint that passes the DNS query to on\-premises DNS servers\.

**EDNS client subnet**  
A partial IP address for the client that the request originated from, if available from the DNS resolver\.  
For more information, see the IETF draft [Client Subnet in DNS Requests](https://tools.ietf.org/html/draft-ietf-dnsop-edns-client-subnet-08)\.