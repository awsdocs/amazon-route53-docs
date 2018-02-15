# Using AWS CloudTrail to Capture Requests Sent to the Amazon Route 53 API<a name="logging-using-cloudtrail"></a>

Amazon Route 53 is integrated with AWS CloudTrail, a service that captures information about every request that is sent to the Route 53 API by your AWS account, including requests that are sent by your IAM users\. CloudTrail periodically saves log files of these requests to an Amazon S3 bucket that you specify\. CloudTrail captures information about all requests, whether they were sent by using the Route 53 console, the Route 53 API, the AWS SDKs, the Route 53 CLI, or another service, such as AWS CloudFormation\.

You can use information in the CloudTrail log files to determine which requests were sent to Route 53, the source IP address that the request was sent from, who sent the request, when it was sent, and so on\. To learn more about CloudTrail, including how to configure and enable it, see the [http://docs.aws.amazon.com/awscloudtrail/latest/userguide/](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.


+ [Configuring CloudTrail for Amazon Route 53](#cloudtrail-configuring-for-route-53)
+ [Amazon Route 53 Information in CloudTrail Log Files](#cloudtrail-route-53-info-in-logs)
+ [Understanding Amazon Route 53 Log File Entries](#cloudtrail-understanding-route-53-entries)

## Configuring CloudTrail for Amazon Route 53<a name="cloudtrail-configuring-for-route-53"></a>

When you configure CloudTrail to capture information about API requests sent by AWS accounts, you start by choosing a region\. For Amazon Route 53, you must choose **US East \(N\. Virginia\)** as the region, or you won't get any log entries for Route 53 API requests\. 

## Amazon Route 53 Information in CloudTrail Log Files<a name="cloudtrail-route-53-info-in-logs"></a>

When you enable CloudTrail, CloudTrail captures every request sent to every AWS service that CloudTrail supports\. \(For a list of supported services, see [Supported Services](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/what_is_cloud_trail_supported_services.html) in the *AWS CloudTrail User Guide*\.\) The log files aren't organized or sorted by service; each log file might contain records from more than one service\. CloudTrail determines when to create a new log file\.

Every log file entry contains information about who sent the request\. The user identity information in the log file helps you determine whether the request was sent by a user with root or IAM user credentials, by a user with temporary security credentials, or by another AWS service, such as AWS CloudFormation\. For more information, see [userIdentity Element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/event_reference_user_identity.html) in the *AWS CloudTrail User Guide*\.

You can store log files for as long as you want\. You can also define Amazon S3 lifecycle rules to archive or delete log files automatically\.

By default, your log files are encrypted by using Amazon S3 server\-side encryption \(SSE\)\.

If you want to review log files as soon as CloudTrail delivers them to your Amazon S3 bucket, you can choose to have CloudTrail publish Amazon SNS notifications when new log files are delivered\. For more information, see [Configuring Amazon SNS Notifications](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html) in the *AWS CloudTrail User Guide*\.

You can also aggregate log files from multiple AWS regions and multiple AWS accounts into a single Amazon S3 bucket\. For more information, see [Aggregating CloudTrail Log Files to a Single Amazon S3 Bucket](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/aggregating_logs_top_level.html) in the *AWS CloudTrail User Guide*\. 

## Understanding Amazon Route 53 Log File Entries<a name="cloudtrail-understanding-route-53-entries"></a>

Each JSON\-formatted CloudTrail log file can contain one or more log entries\. A log entry represents a single request from any source and includes information about the requested action, including any parameters, the date and time of the action, and so on\. The log entries are not guaranteed to be in any particular order; they are not an ordered stack trace of API calls\.

**Important**  
Don't use CloudTrail log entries to reconstruct a hosted zone or to revert a hosted zone to a prior state\. Although extremely rare, it is possible that an Amazon Route 53 API request is not successfully recorded in the CloudTrail log\. If you try to reproduce a hosted zone and a log entry is missing, the record that you don't create or update could adversely affect the availability of your domain\.

The `eventName` element identifies the action that occurred\. \(In CloudTrail logs, the first letter is lowercase for domain registration actions even though it's uppercase in the names of the actions\. For example, `UpdateDomainContact` appears as `updateDomainContact` in the logs\)\. CloudTrail supports all Route 53 API actions\. The following example shows a CloudTrail log entry that demonstrates the following actions:

+ Listing the hosted zones that are associated with an AWS account

+ Creating a health check

+ Creating two records

+ Deleting a hosted zone

+ Creating a public namespace for autonaming

+ Updating information for a registered domain

```
{
    "Records": [
        {
            "apiVersion": "2013-04-01",
            "awsRegion": "us-east-1",
            "eventID": "1cdbea14-e162-43bb-8853-f9f86d4739ca",
            "eventName": "ListHostedZones",
            "eventSource": "route53.amazonaws.com",
            "eventTime": "2015-01-16T00:41:48Z",
            "eventType": "AwsApiCall",
            "eventVersion": "1.02",
            "recipientAccountId": "444455556666",
            "requestID": "741e0df7-9d18-11e4-b752-f9c6311f3510",
            "requestParameters": null,
            "responseElements": null,
            "sourceIPAddress": "192.0.2.92",
            "userAgent": "Apache-HttpClient/4.3 (java 1.5)",
            "userIdentity": {
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
                "accountId": "111122223333",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "type": "IAMUser",
                "userName": "smithj"
            }
        },
        {
            "apiVersion": "2013-04-01",
            "awsRegion": "us-east-1",
            "eventID": "45ec906a-1325-4f61-b133-3ef1012b0cbc",
            "eventName": "CreateHealthCheck",
            "eventSource": "route53.amazonaws.com",
            "eventTime": "2018-01-16T00:41:57Z",
            "eventType": "AwsApiCall",
            "eventVersion": "1.02",
            "recipientAccountId": "444455556666",
            "requestID": "79915168-9d18-11e4-b752-f9c6311f3510",
            "requestParameters": {
                "callerReference": "2014-05-06 64832",
                "healthCheckConfig": {
                    "iPAddress": "192.0.2.249",
                    "port": 80,
                    "type": "TCP"
                }
            },
            "responseElements": {
                "healthCheck": {
                    "callerReference": "2014-05-06 64847",
                    "healthCheckConfig": {
                        "failureThreshold": 3,
                        "iPAddress": "192.0.2.249",
                        "port": 80,
                        "requestInterval": 30,
                        "type": "TCP"
                    },
                    "healthCheckVersion": 1,
                    "id": "b3c9cbc6-cd18-43bc-93f8-9e557example"
                },
                "location": "https://route53.amazonaws.com/2013-04-01/healthcheck/b3c9cbc6-cd18-43bc-93f8-9e557example"
            },
            "sourceIPAddress": "192.0.2.92",
            "userAgent": "Apache-HttpClient/4.3 (java 1.5)",
            "userIdentity": {
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
                "accountId": "111122223333",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "type": "IAMUser",
                "userName": "smithj"
            }
        },
        {
            "additionalEventData": {
                "Note": "Do not use to reconstruct hosted zone"
            },
            "apiVersion": "2013-04-01",
            "awsRegion": "us-east-1",
            "eventID": "883b14d9-2f84-4005-8bc5-c7bf0cebc116",
            "eventName": "ChangeResourceRecordSets",
            "eventSource": "route53.amazonaws.com",
            "eventTime": "2018-01-16T00:41:43Z",
            "eventType": "AwsApiCall",
            "eventVersion": "1.02",
            "recipientAccountId": "444455556666",
            "requestID": "7081d4c6-9d18-11e4-b752-f9c6311f3510",
            "requestParameters": {
                "changeBatch": {
                    "changes": [
                        {
                            "action": "CREATE",
                            "resourceRecordSet": {
                                "name": "prod.example.com.",
                                "resourceRecords": [
                                    {
                                        "value": "192.0.1.1"
                                    },
                                    {
                                        "value": "192.0.1.2"
                                    },
                                    {
                                        "value": "192.0.1.3"
                                    },
                                    {
                                        "value": "192.0.1.4"
                                    }
                                ],
                                "tTL": 300,
                                "type": "A"
                            }
                        },
                        {
                            "action": "CREATE",
                            "resourceRecordSet": {
                                "name": "test.example.com.",
                                "resourceRecords": [
                                    {
                                        "value": "192.0.1.1"
                                    },
                                    {
                                        "value": "192.0.1.2"
                                    },
                                    {
                                        "value": "192.0.1.3"
                                    },
                                    {
                                        "value": "192.0.1.4"
                                    }
                                ],
                                "tTL": 300,
                                "type": "A"
                            }
                        }
                    ],
                    "comment": "Adding subdomains"
                },
                "hostedZoneId": "Z1PA6795UKMFR9"
            },
            "responseElements": {
                "changeInfo": {
                    "comment": "Adding subdomains",
                    "id": "/change/C156SRE0X2ZB10",
                    "status": "PENDING",
                    "submittedAt": "Jan 16, 2018 12:41:43 AM"
                }
            },
            "sourceIPAddress": "192.0.2.92",
            "userAgent": "Apache-HttpClient/4.3 (java 1.5)",
            "userIdentity": {
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
                "accountId": "111122223333",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "type": "IAMUser",
                "userName": "smithj"
            }
        },
        {
            "apiVersion": "2013-04-01",
            "awsRegion": "us-east-1",
            "eventID": "0cb87544-ebee-40a9-9812-e9dda1962cb2",
            "eventName": "DeleteHostedZone",
            "eventSource": "route53.amazonaws.com",
            "eventTime": "2018-01-16T00:41:37Z",
            "eventType": "AwsApiCall",
            "eventVersion": "1.02",
            "recipientAccountId": "444455556666",
            "requestID": "6d5d149f-9d18-11e4-b752-f9c6311f3510",
            "requestParameters": {
                "id": "Z1PA6795UKMFR9"
            },
            "responseElements": {
                "changeInfo": {
                    "id": "/change/C1SIJYUYIKVJWP",
                    "status": "PENDING",
                    "submittedAt": "Jan 16, 2018 12:41:36 AM"
                }
            },
            "sourceIPAddress": "192.0.2.92",
            "userAgent": "Apache-HttpClient/4.3 (java 1.5)",
            "userIdentity": {
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
                "accountId": "111122223333",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "type": "IAMUser",
                "userName": "smithj"
            }
        },
        {
            "eventVersion": "1.05",
            "userIdentity": {
                "type": "IAMUser",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "accountId": "111122223333",
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
                "userName": "smithj"
            },
            "eventTime": "2018-01-16T00:44:17Z",
            "eventSource": "servicediscovery.amazonaws.com",
            "eventName": "CreatePublicDnsNamespace",
            "awsRegion": "us-west-2",
            "sourceIPAddress": "192.0.2.92",
            "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.12; rv:52.0) Gecko/20100101 Firefox/52.0",
            "requestParameters": {
                "description": "test",
                "creatorRequestId": "1234567890123456789",
                "name": "example.com"
            },
            "responseElements": {
                "operationId": "unmipghn37443trlkgpf4idvvitec6fw-26514969"
            },
            "requestID": "35e1872d-c0dc-11e7-99e1-03e9f7b7ccdd",
            "eventID": "409b4d91-34e6-41ee-bd97-a816d5d04055",
            "eventType": "AwsApiCall",
            "recipientAccountId": "444455556666"
        },
        {
            "eventVersion": "1.05",
            "userIdentity": {
                "type": "IAMUser",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "accountId": "111122223333",
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE",
                "userName": "smithj",
                "sessionContext": {
                    "attributes": {
                        "mfaAuthenticated": "false",
                        "creationDate": "2017-11-01T19:43:59Z"
                    }
                },
                "invokedBy": "test"
            },
            "eventTime": "2018-01-16T00:49:36Z",
            "eventSource": "route53domains.amazonaws.com",
            "eventName": "updateDomainContact",
            "awsRegion": "us-west-2",
            "sourceIPAddress": "192.0.2.92",
            "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.12; rv:52.0) Gecko/20100101 Firefox/52.0",
            "requestParameters": {
                "domainName": {
                    "name": "example.com"
                }
            },
            "responseElements": {
                "requestId": "034e222b-a3d5-4bec-8ff9-35877ff02187"
            },
            "additionalEventData": "Personally-identifying contact information is not logged in the request",
            "requestID": "015b7313-bf3d-11e7-af12-cf75409087f6",
            "eventID": "f34f3338-aaf4-446f-bf0e-f72323bac94d",
            "eventType": "AwsApiCall",
            "recipientAccountId": "444455556666"
        }
    ]
}
```