# Resolver endpoint scaling<a name="best-practices-resolver-endpoint-scaling"></a>

Resolver endpoint security groups use connection tracking to gather information about traffic to and from the endpoints\. Each endpoint interface has a maximum number of connections that can be tracked, and a high volume of DNS queries can exceed the connections and cause throttling and query loss\. To reduce the number of connections that are tracked, implement security group rules that permit traffic based on the connection state of the traffic\. For more information, see [ Security groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html) and [ Connection tracking](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-connection-tracking.html) in *Amazon EC2 User Guide for Linux Instances *\.

**Inbound and Outbound Resolver security group recommendations**


****  

| 
| 
| **Inbound rules** | 
| --- |
| Protocol type | Port number | Source IP | 
| TCP  | 53 | 0\.0\.0\.0/0 | 
| UDP | 53 | 0\.0\.0\.0/0 | 
| **Outbound rules** | 
| --- |
| Protocol type | Port number | Destination IP | 
| TCP | All | 0\.0\.0\.0/0 | 
| UDP | All | 0\.0\.0\.0/0 | 

**Inbound Resolver endpoints**

For clients using an inbound resolver endpoint, the capacity of the elastic network interface will be impacted if you have over 40,000 unique IP address and port combinations generating the DNS traffic\.