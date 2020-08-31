# AWS resources that you can send Resolver query logs to<a name="resolver-query-logs-choosing-target-resource"></a>

**Note**  
If you expect to log queries for workloads with high queries per second \(QPS\), you should use Amazon S3 to ensure your query logs are not throttled when written to your destination\. If you use Amazon CloudWatch, you can increase your requests per second limit for the `PutLogEvents` operation\. To learn more about increasing your CloudWatch limits, see [CloudWatch Logs quotas](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/cloudwatch_limits_cwl.html) in the *Amazon CloudWatch User Guide*\.

You can send Resolver query logs to the following AWS resources:

**Amazon CloudWatch Logs \(Amazon CloudWatch Logs\) log group**  
You can analyze logs with Logs Insights and create metrics and alarms\.  
For more information, see the [Amazon CloudWatch Logs User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/)\.

**Amazon S3 \(S3\) bucket**  
An S3 bucket is economical for long\-term log archiving\. Latency is typically higher\.  
For more information, see the [Amazon Simple Storage Service Console User Guide](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/)\.

**Kinesis Data Firehose delivery stream**  
You can stream logs in real time to Elasticsearch, Redshift, or other applications\.  
For more information, see the [Amazon Kinesis Data Firehose Developer Guide](https://docs.aws.amazon.com/firehose/latest/dev/)\.

For information about the pricing for Resolver query logging, see [Amazon CloudWatch pricing](http://aws.amazon.com/cloudwatch/pricing/)\.