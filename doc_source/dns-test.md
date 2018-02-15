# Checking DNS Responses from Route 53<a name="dns-test"></a>

If you created an Amazon Route 53 hosted zone for your domain, you can use the DNS checking tool in the console to see how Route 53 will respond to DNS queries if you configure your domain to use Route 53 as your DNS service\. For geolocation and latency records, you can also simulate queries from a particular DNS resolver and/or client IP address to find out what response Route 53 would return\.

**Important**  
The DNS checking tool does not indicate whether Route 53 is currently the DNS service for your domain\. Responses from the tool are based only on the settings in your hosted zone, not on responses from the Domain Name System\.

The DNS checking tool works only for public hosted zones\.


+ [Using the Checking Tool to See How Amazon Route 53 Responds to DNS Queries](#dns-test-how-route-53-responds)
+ [Using the Checking Tool to Simulate Queries from Specific IP Addresses \(Geolocation and Latency Records Only\)](#dns-test-simulate-requests)

## Using the Checking Tool to See How Amazon Route 53 Responds to DNS Queries<a name="dns-test-how-route-53-responds"></a>

You can use the tool to see what response Amazon Route 53 returns in response to a DNS query for a record\.

**To use the checking tool to see how Route 53 responds to DNS queries**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. On the **Hosted Zones** page, choose the name of a hosted zone\. The console displays the list of records for that hosted zone\.

1. To go directly to the **Check response from Route 53** page, choose **Test record set**\.

   To go to the **Check response from Route 53** page for a specific record, choose the check box for that record and choose **Test record set**\.

1. If you chose **Test record set** without first choosing a record, specify the name and type of the record\.

1. Choose **Get Response**\.

1. The **Response returned by Route 53** section includes the following values:  
**DNS query sent to Route 53**  
The query, in [BIND format](https://en.wikipedia.org/wiki/Zone_file), that the checking tool sent to Route 53\. This is the same format that a web application would use to send a query\. The three values are typically the name of the record, **IN** \(for internet\), and the type of the record\.  
**DNS response code**  
A code that indicates whether the query was valid or not\. The most common response code is **NOERROR**, meaning that the query was valid\. If the response is not valid, Route 53 returns a response code that explains why not\. For a list of possible response codes, see [DNS RCODES](http://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6) on the IANA website\.  
**Protocol**  
The protocol that Amazon Route 53 used to respond to the query, either **UDP** or **TCP**\.  
**Response returned by Route 53**  
The value that Route 53 would return to a web application\. The value is one of the following:  

   + For non\-alias records, the response contains the value or values in the record\.

   + For multiple records that have the same name and type, which includes weighted, latency, geolocation, and failover, the response contains the value from the appropriate record, based on the request\. 

   + For alias records that refer to AWS resources other than another record, the response contains an IP address or a domain name for the AWS resource, depending on the type of resource\.

   + For alias records that refer to other records, the response contains the value or values from the referenced record\.

## Using the Checking Tool to Simulate Queries from Specific IP Addresses \(Geolocation and Latency Records Only\)<a name="dns-test-simulate-requests"></a>

If you have created latency or geolocation records, you can use the checking tool to simulate queries from the IP address for a DNS resolver and a client\.

**To use the checking tool to simulate queries from specified IP addresses**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. On the **Hosted Zones** page, choose the name of a hosted zone\. The console displays the list of records for that hosted zone\.

1. To go directly to the **Check response from Route 53** page, choose **Test record set**\.

   To go to the **Check response from Route 53** page for a specific record, choose the check box for that record and choose **Test record set**\.

1. If you chose **Test record set** without first choosing a record, specify the name and type of the record\.

1. Specify the applicable values:  
**Resolver IP address**  
Specify an IPv4 or IPv6 address to simulate the location of the DNS resolver that a client uses to make requests\. This is useful for testing latency and geolocation records\. If you omit this value, the tool uses the IP address of a DNS resolver in the AWS US East \(N\. Virginia\) Region \(us\-east\-1\)\.   
**EDNS0 client subnet IP**  
If the resolver supports EDNS0, type the client subnet IP for an IP address in the applicable geographic location, for example, **192\.0\.2\.0** or **2001:db8:85a3::8a2e:370:7334**\.   
**Subnet mask**  
If you specify an IP address for **EDNS0 client subnet IP**, you can optionally specify the number of bits of the IP address that you want the checking tool to include in the DNS query\. For example, if you specify **192\.0\.2\.44** for **EDNS0 client subnet IP** and **24** for **Subnet mask**, the checking tool will simulate a query from **192\.0\.2\.0/24**\. The default value is 24 bits for IPv4 addresses and 64 bits for IPv6 addresses\. 

1. Choose **Get Response**\.

1. The **Response returned by Route 53** section includes the following values:  
**DNS query sent to Route 53**  
The query, in [BIND format](https://en.wikipedia.org/wiki/Zone_file), that the checking tool sent to Route 53\. This is the same format that a web application would use to send a query\. The three values are typically the name of the record, **IN** \(for internet\), and the type of the record\.  
**DNS response code**  
A code that indicates whether the query was valid or not\. The most common response code is **NOERROR**, meaning that the query was valid\. If the response is not valid, Route 53 returns a response code that explains why not\. For a list of possible response codes, see [DNS RCODES](http://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6) on the IANA website\.  
**Protocol**  
The protocol that Amazon Route 53 used to respond to the query, either **UDP** or **TCP**\.  
**Response returned by Route 53**  
The value that Route 53 would return to a web application\. The value is one of the following:  

   + For non\-alias records, the response contains the value or values in the record\.

   + For multiple records that have the same name and type, which includes weighted, latency, geolocation, and failover, the response contains the value from the appropriate record, based on the request\. 

   + For alias records that refer to AWS resources other than another record, the response contains an IP address or a domain name for the AWS resource, depending on the type of resource\.

   + For alias records that refer to other records, the response contains the value or values from the referenced record\.