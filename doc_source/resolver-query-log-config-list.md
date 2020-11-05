# Query logging configurations<a name="resolver-query-log-config-list"></a>

The list of query logging configurations includes the following information about the existing configurations:
+ **Name**: The name that you assigned to the configuration when you created it\.
+ **ID**: The ID that Resolver assigned to the configuration when you created it\. This value is mainly used to access the configuration programmatically\.
+ **Status**: The current status of the configuration\. Values include the following:
  + **Active**: The configuration was successfully created, and one or more VPCs are associated with it\. The configuration is logging DNS queries that originate in those VPCs\.
  + **Creating**: Resolver is creating the configuration\.
  + **Created**: The configuration was successfully created\. No VPCs are associated with the configuration, so the configuration isn't logging queries\. 
  + **Deleting**: Resolver is deleting the configuration\.
  + **Failed**: Resolver can't deliver logs to the destination because the destination \(such as an S3 bucket\) has been deleted or permissions don't allow saving logs in the destination\.
+ **Destination type**: The type of AWS resource that the configuration is saving logs in, an Amazon CloudWatch Logs \(CloudWatch Logs\) log group, an Amazon S3 bucket, or Amazon Kinesis Data Firehose \(Kinesis Data Firehose\) delivery stream\.
+ **Destination ARN**: The ARN of the specific resource that the configuration is saving logs in, for example, the ARN of an S3 bucket\.
+ **VPC count**: The number of VPCs that the query logging configuration is logging DNS queries for\.
+ **Sharing status**: Indicates whether the configuration is shared with other AWS accounts\.

## Learn more<a name="resolver-query-log-config-list-learn-more"></a>
+ [Resolver query Logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html)
+ [AWS resources that you can send Resolver query logs to](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html#resolver-query-logs-choosing-target-resource)