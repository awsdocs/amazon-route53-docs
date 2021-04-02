# AWS resources that you can send Resolver query logs to<a name="resolver-query-logs-choosing-target-resource"></a>

**Note**  
If you expect to log queries for workloads with high queries per second \(QPS\), you should use Amazon S3 to ensure your query logs are not throttled when written to your destination\. If you use Amazon CloudWatch, you can increase your requests per second limit for the `PutLogEvents` operation\. To learn more about increasing your CloudWatch limits, see [CloudWatch Logs quotas](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/cloudwatch_limits_cwl.html) in the *Amazon CloudWatch User Guide*\.

You can send Resolver query logs to the following AWS resources:

**Amazon CloudWatch Logs \(Amazon CloudWatch Logs\) log group**  
You can analyze logs with Logs Insights and create metrics and alarms\.  
For more information, see the [Amazon CloudWatch Logs User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/)\.

**Amazon S3 \(S3\) bucket**  
An S3 bucket is economical for long\-term log archiving\. Latency is typically higher\.  
If you want to send logs to an S3 bucket in an account that you don't own, the owner of the S3 bucket must add permissions for your account in their bucket policy\. For example:  

```
{
    "Version": "2012-10-17",
    "Id": "CrossAccountAccess",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::your_bucket_name/AWSLogs/your_caller_account/*"
        }
    ]
}
```
 If you want to store logs in a central S3 bucket for your organization, we recommend that you set up your query logging configuration from a centralized account \(with the necessary permissions to write to a central bucket\) and use [RAM](query-logging-configurations-managing-sharing.md) to share the configuration across accounts\.
For more information, see the [Amazon Simple Storage Service Console User Guide](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/)\.

**Kinesis Data Firehose delivery stream**  
You can stream logs in real time to Elasticsearch, Amazon Redshift, or other applications\.  
For more information, see the [Amazon Kinesis Data Firehose Developer Guide](https://docs.aws.amazon.com/firehose/latest/dev/)\.

For information about the pricing for Resolver query logging, see [Amazon CloudWatch pricing](http://aws.amazon.com/cloudwatch/pricing/)\.