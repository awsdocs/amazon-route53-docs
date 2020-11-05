# Query logs destination<a name="resolver-query-log-config-destination"></a>

Choose the type of resource that you want Resolver to send DNS query logs to:
+ **Amazon CloudWatch Logs log group**: If you save logs in a log group, you can analyze logs with Logs Insights and create metrics and alarms\.
+ **Amazon S3 bucket**: Saving logs in an S3 bucket is economical for long\-term log archiving\. Latency for retrieving logs is typically higher\.
+ **Amazon Kinesis Data Firehose delivery stream**: If you choose this option, you can stream logs in real time to Amazon Elasticsearch Service, Amazon Redshift, or other applications\.

After you choose the type of resource, you can choose a specific resource of that type, or create a new one\.

**Note**  
If you choose to save logs in an S3 bucket, you can also specify an optional filename prefix\. The prefix is prepended to the name of every log file in the S3 bucket that you choose\. 

## Learn more<a name="resolver-query-log-config-destination-learn-more"></a>
+ [Resolver query Logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html)
+ [Resolver query Logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html)
+ [Configuring Resolver query logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html#resolver-query-logs-configuring)
+ [AWS resources that you can send Resolver query logs to](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html#resolver-query-logs-choosing-target-resource)