# Configuration details<a name="resolver-query-log-config-detail"></a>

The details page for a query logging configuration includes the following information:
+ **ID**: The ID that Resolver assigned to the configuration when you created it\. This value is mainly used to access the configuration programmatically\.
+ **Destination type**: The type of AWS resource that the configuration is saving logs in, an Amazon CloudWatch Logs \(CloudWatch Logs\) log group, an Amazon S3 \(S3\) bucket, or an Amazon Kinesis Data Firehose \(Kinesis Data Firehose\) delivery stream\.
+ **Destination ARN**: The ARN of the specific resource that the configuration is saving logs in, for example, the ARN of an S3 bucket\.
+ **Status**: The current status of the configuration\. Values include the following:
  + **Active**: The configuration was successfully created, and one or more VPCs are associated with it\. The configuration is logging DNS queries that originate in those VPCs\.
  + **Creating**: Resolver is creating the configuration\.
  + **Created**: The configuration was successfully created\. No VPCs are associated with the configuration, so the configuration isn't logging queries\. 
  + **Deleting**: Resolver is deleting the configuration\.
  + **Failed**: Resolver can't deliver logs to the destination because the destination \(such as an S3 bucket\) has been deleted or permissions don't allow saving logs in the destination\.
+ **VPC count**: The number of VPCs that the query logging configuration is logging DNS queries for\.
+ **Creation Time \(UTC\)**: The date and time that the configuration was created in Coordinated Universal Time \(UTC\) and in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601)\.
+ **Sharing status**: Indicates whether the configuration is shared with other AWS accounts\. Valid values include the following:
  + **Not shared**: The configuration was created by the current account and is not shared with any other AWS accounts\.
  + **Shared by me**: The configuration was created by the current account and is shared with one or more other AWS accounts\.
  + **Shared with me**: The configuration was created by another account and is shared with the current account\. 
+ **Owner**: The value of **Owner** depends on the value of **Sharing status**:
  + **Not shared**: The value of **Owner** is the ID of the current account\.
  + **Shared by me**: The value of **Owner** is the ID of the current account\.
  + **Shared with me**: The value of **Owner** is the ID of the account that created the configuration and shared it with the current account\.
+ **ARN**:

## Learn more<a name="resolver-query-log-config-detail-learn-more"></a>
+ [Resolver query Logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html)
+ [AWS resources that you can send Resolver query logs to](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html#resolver-query-logs-choosing-target-resource)