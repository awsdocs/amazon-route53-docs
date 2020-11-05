# Subnet mask<a name="record-test-subnet-mask"></a>

If you specify an IP address for **EDNS0 client subnet IP**, you can optionally specify the number of bits of the IP address that you want the checking tool to include in the DNS query\. For example, if you specify **192\.0\.2\.44** for **EDNS0 client subnet IP** and **24** for **Subnet mask**, the checking tool will simulate a query from **192\.0\.2\.0/24**\. The default value is 24 bits for IPv4 addresses and 64 bits for IPv6 addresses\. 

## Learn more<a name="record-test-subnet-mask-learn-more"></a>
+ [Using the checking tool to simulate queries from specific IP addresses](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-test.html#dns-test-simulate-requests)
+ [How Amazon Route 53 uses EDNS0 to estimate the location of a user](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html#routing-policy-edns0)