# Configuring router and firewall rules for Amazon Route 53 health checks<a name="dns-failover-router-firewall-rules"></a>

When Route 53 checks the health of an endpoint, it sends an HTTP, HTTPS, or TCP request to the IP address and port that you specified when you created the health check\. For a health check to succeed, your router and firewall rules must allow inbound traffic from the IP addresses that the Route 53 health checkers use\. \(In Amazon EC2, security groups act as firewalls\. For more information, see [Amazon EC2 security groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html) in the *Amazon EC2 User Guide for Linux Instances*\.\)

For the current list of IP addresses for Route 53 health checkers, for Route 53 name servers, and for other AWS services, see [IP address ranges of Amazon Route 53 servers](route-53-ip-addresses.md)\. 

**Important**  
When you add IP addresses to a list of allowed IP addresses, add all the IP addresses in the CIDR range for each AWS Region that you specified when you created health checks\. You might see that health check requests come from just one IP address in a Region\. However, that IP address can change at any time to another of the IP addresses for that Region\.