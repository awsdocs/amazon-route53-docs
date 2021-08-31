# Values that appear in Resolver query logs<a name="resolver-query-logs-format"></a>

Each log file contains one log entry for each DNS query that Amazon Route 53 received from DNS resolvers in the corresponding edge location\. Each log entry includes the following values:

**version**  
The version number of the query log format\. The current version is `1.1`\.  
The version value is a major and minor version in the form **major\_version\.minor\_version**\. For example, you can have a `version` value of `1.7`, where `1 `is the major version, and `7` is the minor version\.  
Route 53 increments the major version if a change is made to the log structure that is not backward\-compatible\. This includes removing a JSON field that already exists, or changing how the contents of a field are represented \(for example, a date format\)\.  
 Route 53 increments the minor version if a change adds new fields to the log file\. This can occur if new information is available for some or all existing DNS queries within a VPC\. 

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
Either the DNS record type that was specified in the request, or `ANY`\. For information about the types that Route 53 supports, see [Supported DNS record types](ResourceRecordTypes.md)\.

**query\_class**  
The class of the query\.

**rcode**  
The DNS response code that Resolver returned in response to the DNS query\. The response code indicates whether the query was valid or not\. The most common response code is `NOERROR`, meaning that the query was valid\. If the response is not valid, Resolver returns a response code that explains why not\. For a list of possible response codes, see [DNS RCODEs](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6) on the IANA website\.

**answer\_type**  
The DNS record type \(such as A, MX, or CNAME\) of the value that Resolver is returning in response to the query\. For information about the types that Route 53 supports, see [Supported DNS record types](ResourceRecordTypes.md)\.

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

**resolver\_endpoint**  
The ID of the resolver endpoint that passes the DNS query to on\-premises DNS servers\.

**firewall\_rule\_group\_id**  
The ID of the DNS Firewall rule group that matched the domain name in the query\. This is populated only if DNS Firewall found a match for a rule with action set to alert or block\.  
For more information about the firewall rule groups, see [DNS Firewall rule groups and rules](resolver-dns-firewall-rule-groups.md)\.

**firewall\_rule\_action**  
The action specified by the rule that matched the domain name in the query\. This is populated only if DNS Firewall found a match for a rule with action set to alert or block\.

**firewall\_domain\_list\_id**  
The domain list used by the rule that matched the domain name in the query\. This is populated only if DNS Firewall found a match for a rule with action set to alert or block\.