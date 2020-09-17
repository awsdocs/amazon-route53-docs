# Logging and monitoring in Amazon Route 53<a name="logging-monitoring"></a>

Amazon Route 53 provides DNS query logging and the ability to monitor your resources using health checks\. In addition, Route 53 integrates with other AWS services to provide additional logging and monitoring:

**Logging DNS queries**  
You can configure Route 53 to log information about the queries that Route 53 receives, such as the domain or subdomain that was requested, the date and time of the request, and the DNS record type, such as A or AAAA\.  
For more information, see [Public DNS query logging](query-logs.md)\.

**Using AWS CloudTrail to log console and programmatic actions**  
CloudTrail provides a record of Route 53 actions taken by a user, a role, or an AWS service\. Using the information collected by CloudTrail, you can track the requests that are made, the IP addresses that requests originate from, who made the request, when it was made, and additional details\. For more information, see [Logging Amazon Route 53 API calls with AWS CloudTrail](logging-using-cloudtrail.md)\.

**Monitoring domain registrations**  
The Route 53 dashboard provides detailed information about the status of your domain registrations, such as the status of domain transfers and domains that are approaching the expiration date\.  
For more information, see [Monitoring domain registrations](monitoring-domain-registrations.md)\.

**Using Route 53 health checks and Amazon CloudWatch to monitor your resources**  
You can monitor your resources by creating Route 53 health checks, which use CloudWatch to collect and process raw data into readable, near real\-time metrics\.  
For more information, see [Monitoring your resources with Amazon Route 53 health checks and Amazon CloudWatch](monitoring-cloudwatch.md)\.

**Using Amazon CloudWatch to monitor Route 53 Resolver endpoints**  
You can use CloudWatch to monitor the number of DNS queries that are forwarded by Resolver endpoints\.  
For more information, see [Monitoring Route 53 Resolver endpoints with Amazon CloudWatch](monitoring-resolver-with-cloudwatch.md)\.

**Using AWS Trusted Advisor**  
Trusted Advisor draws upon best practices learned from serving AWS customers\. Trusted Advisor inspects your AWS environment and then makes recommendations when opportunities exist to save money, improve system availability and performance, or help close security gaps\. All AWS customers have access to five Trusted Advisor checks\. Customers with a Business or Enterprise support plan can view all Trusted Advisor checks\.  
For more information, see [Trusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/getting-started.html#trusted-advisor)\.