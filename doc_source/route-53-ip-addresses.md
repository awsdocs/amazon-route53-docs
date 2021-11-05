# IP address ranges of Amazon Route 53 servers<a name="route-53-ip-addresses"></a>

Amazon Web Services \(AWS\) publishes its current IP address ranges in JSON format\. If your firewalls or security groups restrict incoming traffic based on source IP addresses, confirm that your configuration allows traffic from the applicable IP address ranges\.

To view the current IP address ranges for Route 53, download [ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json), and search the file for the following values:

**`"service": "ROUTE53"`**  
These IP address ranges are used by Route 53 name servers\. Add these ranges to the list of allowed IP address ranges if you're using Route 53 as the DNS service for one or more domains and you want to be able to use the `dig` or `nslookup` commands to query Route 53 name servers\.  
We rarely change the IP addresses of name servers; if we need to change IP addresses, we'll notify you in advance\.

**`"service": "ROUTE53_HEALTHCHECKS"`**  
These IP address ranges are used by Route 53 health checkers\. Add these ranges to the list of allowed IP address ranges if you're using Route 53 health checks to check the health of resources on your network\.  
We rarely change the IP addresses of health checkers; if we need to change IP addresses, we'll notify you in advance\.
For more information about IP addresses for health checks, see [Configuring router and firewall rules for Amazon Route 53 health checksConfiguring router and firewall rules for health checks](dns-failover-router-firewall-rules.md)\.

**`"service": "ROUTE53_HEALTHCHECKS_PUBLISHING"`**  
Route 53 uses these IP address ranges only internally\. You don't need to add these ranges to the list of allowed ranges\.

For more information about IP addresses for AWS resources, see [AWS IP address ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html) in the *Amazon Web Services General Reference*\. 