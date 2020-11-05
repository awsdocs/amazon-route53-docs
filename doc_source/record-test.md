# Test record<a name="record-test"></a>

Test record shows how Route 53 responds to DNS queries for a specified record\. For geolocation, geoproximity, and latency records, you can also simulate queries from a particular DNS resolver and/or client IP address to find out what response Route 53 would return\.

**Important**  
The tool doesn't submit queries to the Domain Name System, it responds based only on the settings in the records in the hosted zone\. The tool returns the same information regardless of whether the hosted zone is currently being used to route traffic for the domain\.

## Learn more<a name="record-test-learn-more"></a>
+ [Checking DNS responses from Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-test.html)