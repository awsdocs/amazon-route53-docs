# Resolver IP address \(optional\)<a name="record-test-resolver-ip"></a>

If you want to simulate the location that a DNS query originates from, specify the IPv4 or IPv6 address of the DNS resolver that a client uses to make requests\. This is useful for testing geolocation, geoproximity, and latency records\. If you omit this value, the tool uses the IP address of a DNS resolver in the AWS US East \(N\. Virginia\) Region \(us\-east\-1\)\. 

## Learn more<a name="record-test-resolver-ip-learn-more"></a>
+ [Using the checking tool to simulate queries from specific IP addresses](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-test.html#dns-test-simulate-requests)