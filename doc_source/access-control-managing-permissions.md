# Using identity\-based policies \(IAM policies\) for Amazon Route 53<a name="access-control-managing-permissions"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities and thereby grant permissions to perform operations on Amazon Route 53 resources\.

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options to manage access to your Route 53 resources\. For more information, see [Overview of managing access permissions to your Amazon Route 53 resources](access-control-overview.md)\. 

**Note**  
When granting access, the hosted zone and the Amazon VPC must belong to the same partition\. A partition is a group of AWS Regions\. Each AWS account is scoped to one partition\.  
The following are the supported partitions:  
`aws` \- AWS Regions
`aws-cn` \- China Regions
`aws-us-gov` \- AWS GovCloud \(US\) Region
For more information, see [Access Management](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) and [Amazon Route 53 endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/r53.html) in the *AWS General Reference*\.

**Topics**
+ [Permissions required to use the Amazon Route 53 console](#console-required-permissions)
+ [Example permissions for a domain record owner](#example-permissions-record-owner)
+ [Route 53 customer managed key permissions required for DNSSEC signing](#KMS-key-policy-for-DNSSEC)
+ [Customer managed policy examples](#access-policy-examples-for-sdk-cli)

The following example shows a permissions policy\. The `Sid`, or statement ID, is optional:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid" : "AllowPublicHostedZonePermissions",
            "Effect": "Allow",
            "Action": [
                "route53:CreateHostedZone",
                "route53:UpdateHostedZoneComment",
                "route53:GetHostedZone",
                "route53:ListHostedZones",
                "route53:DeleteHostedZone",
                "route53:ChangeResourceRecordSets",
                "route53:ListResourceRecordSets",
                "route53:GetHostedZoneCount",
                "route53:ListHostedZonesByName"
            ],
            "Resource": "*"
        },
        {
         "Sid" : "AllowHealthCheckPermissions",
            "Effect": "Allow",
            "Action": [
                "route53:CreateHealthCheck",
                "route53:UpdateHealthCheck",
                "route53:GetHealthCheck",
                "route53:ListHealthChecks",
                "route53:DeleteHealthCheck",
                "route53:GetCheckerIpRanges",
                "route53:GetHealthCheckCount",
                "route53:GetHealthCheckStatus",
                "route53:GetHealthCheckLastFailureReason"
            ],
            "Resource": "*"
        }
    ]
}
```

The policy includes two statements:
+ The first statement grants permissions to the actions that are required to create and manage public hosted zones and their records\. The wildcard character \(\*\) in the Amazon Resource Name \(ARN\) grants access to all the hosted zones that are owned by the current AWS account\. 
+ The second statement grants permissions to all the actions that are required to create and manage health checks\.

For a list of actions and the ARN that you specify to grant or deny permission to use each action, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md)\.

## Permissions required to use the Amazon Route 53 console<a name="console-required-permissions"></a>

To grant full access to the Amazon Route 53 console, you grant the permissions in the following permissions policy: 

```
{
    "Version": "2012-10-17",
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "route53:*", 
                "route53domains:*",
                "cloudfront:ListDistributions",
                "elasticloadbalancing:DescribeLoadBalancers",
                "elasticbeanstalk:DescribeEnvironments",
                "s3:ListAllMyBuckets",
                "s3:GetBucketLocation",
                "s3:GetBucketWebsite",
                "ec2:DescribeRegions",
                "ec2:DescribeVpcs",
                "ec2:CreateNetworkInterface",
                "ec2:CreateNetworkInterfacePermission",
                "ec2:DeleteNetworkInterface",
                "ec2:DescribeAvailabilityZones",
                "ec2:DescribeNetworkInterfaces",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeSubnets",
                "ec2:ModifyNetworkInterfaceAttribute",
                "sns:ListTopics",
                "sns:ListSubscriptionsByTopic",
                "sns:CreateTopic",
                "kms:ListAliases",
                "kms:DescribeKey",
                "kms:CreateKey",
                "kms:CreateAlias",
                "kms:Sign",
                "cloudwatch:DescribeAlarms",
                "cloudwatch:PutMetricAlarm",
                "cloudwatch:DeleteAlarms",
                "cloudwatch:GetMetricStatistics"
            ],
            "Resource":"*"
        },
        {
            "Effect": "Allow",
            "Action": "apigateway:GET",
            "Resource": "arn:aws:apigateway:*::/domainnames"
        }
    ]
}
```

Here's why the permissions are required:

**`route53:*`**  
Lets you perform all Route 53 actions *except* the following:  
+ Create and update alias records for which the value of **Alias Target** is a CloudFront distribution, an Elastic Load Balancing load balancer, an Elastic Beanstalk environment, or an Amazon S3 bucket\. \(With these permissions, you can create alias records for which the value of **Alias Target** is another record in the same hosted zone\.\)
+ Work with private hosted zones\.
+ Work with domains\.
+ Create, delete, and view CloudWatch alarms\.
+ Render CloudWatch metrics in the Route 53 console\.

**`route53domains:*`**  
Lets you work with domains\.  
If you list `route53` actions individually, you must include `route53:CreateHostedZone` to work with domains\. When you register a domain, a hosted zone is created at the same time, so a policy that includes permissions to register domains also requires permission to create hosted zones\.
For domain registration, Route 53 doesn't support granting or denying permissions to individual resources\.

**`route53resolver:*`**  
Lets you work with Route 53 Resolver\.

**`cloudfront:ListDistributions`**  
Lets you create and update alias records for which the value of **Alias Target** is a CloudFront distribution\.  
These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of distributions to display in the console\.

**`elasticloadbalancing:DescribeLoadBalancers`**  
Lets you create and update alias records for which the value of **Alias Target** is an ELB load balancer\.  
These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of load balancers to display in the console\.

**`elasticbeanstalk:DescribeEnvironments`**  
Lets you create and update alias records for which the value of **Alias Target** is an Elastic Beanstalk environment\.  
These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of environments to display in the console\.

**`s3:ListAllMyBuckets`, `s3:GetBucketLocation`, and `s3:GetBucketWebsite`**  
Let you create and update alias records for which the value of **Alias Target** is an Amazon S3 bucket\. \(You can create an alias to an Amazon S3 bucket only if the bucket is configured as a website endpoint; `s3:GetBucketWebsite` gets the required configuration information\.\)  
These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of buckets to display in the console\.

**`ec2:DescribeVpcs` and `ec2:DescribeRegions`**  
Let you work with private hosted zones\.

**All listed `ec2` permissions**  
Let you work with Route 53 Resolver\.

**`sns:ListTopics`, `sns:ListSubscriptionsByTopic`, `sns:CreateTopic`, `cloudwatch:DescribeAlarms`, `cloudwatch:PutMetricAlarm`, `cloudwatch:DeleteAlarms`**  
Let you create, delete, and view CloudWatch alarms\.

**`cloudwatch:GetMetricStatistics`**  
Lets you create CloudWatch metric health checks\.  
These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get statistics to display in the console\. 

**`apigateway:GET`**  
Lets you create and update alias records for which the value of **Alias Target** is an Amazon API Gateway API\.  
This permission isn't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of APIs to display in the console\.

**`kms:*`**  
Lets you work with AWS KMS to enable DNSSEC signing\.

## Example permissions for a domain record owner<a name="example-permissions-record-owner"></a>

With resource record set permissions you can set granular permissions that limit what the AWS user can update or modify\. For more intormation, see [Using IAM policy conditions for fine\-grained access control to manage resource record sets](specifying-rrset-conditions.md)\.

In some scenarios, a hosted zone owner might be responsible for the overall management of the hosted zone, while another person in the organization is responsible for a subset of those tasks\. A hosted zone owner who has enabled DNSSEC signing, for example, might want to create an IAM policy that includes the permission for someone else to add and delete Resource Set Records \(RRs\) in the hosted zone, among other tasks\. The specific permissions that a hosted zone owner chooses to enable for a record owner or other people will depend on their organization's policy\.

The following is an example IAM policy that allows a record owner to make modifications to RRs, traffic policies, and health checks\. A record owner with this policy is not allowed to do zone\-level operations, such as creating or deleting a zone, enabling or disabling query logging, creating or deleting a reusable delegation set, or changing DNSSEC settings\.

```
{
      "Sid": "Do not allow zone-level modification ",
      "Effect": "Allow",
      "Action": [
        "route53:ChangeResourceRecordSets",
        "route53:CreateTrafficPolicy",
        "route53:DeleteTrafficPolicy",
        "route53:CreateTrafficPolicyInstance",
        "route53:CreateTrafficPolicyVersion",
        "route53:UpdateTrafficPolicyInstance",
        "route53:UpdateTrafficPolicyComment",
        "route53:DeleteTrafficPolicyInstance",
        "route53:CreateHealthCheck",
        "route53:UpdateHealthCheck",
        "route53:DeleteHealthCheck",
        "route53:List*",
        "route53:Get*"
      ],
      "Resource": [
        "*"
      ]
}
```

## Route 53 customer managed key permissions required for DNSSEC signing<a name="KMS-key-policy-for-DNSSEC"></a>

When you enable DNSSEC signing for Route 53, Route 53 creates a key\-signing key \(KSK\) based on a customer managed key in AWS Key Management Service \(AWS KMS\)\. You can use an existing customer managed key that supports DNSSEC signing or create a new one\. Route 53 must have permission to access your customer managed key so that it can create the KSK for you\. 

To enable Route 53 to access your customer managed key, make sure that your customer managed key policy contains the following statements:

```
{
            "Sid": "Allow Route 53 DNSSEC Service",
            "Effect": "Allow",
            "Principal": {
                "Service": "dnssec-route53.amazonaws.com"
            },
            "Action": ["kms:DescribeKey",
                       "kms:GetPublicKey",
                       "kms:Sign"],
            "Resource": "*"
        },
        {
            "Sid": "Allow Route 53 DNSSEC to CreateGrant",
            "Effect": "Allow",
            "Principal": {
                "Service": "dnssec-route53.amazonaws.com"
            },
            "Action": ["kms:CreateGrant"],
            "Resource": "*",
            "Condition": {
                "Bool": {
                    "kms:GrantIsForAWSResource": true
                }
            }
        }
```

The confused deputy problem is a security issue where an entity without a permission for an action can coerce a more\-privileged entity to perform it\. To protect your AWS KMS from it, you can optionally limit the permissions that a service has to a resource in a resource\-based policy by supplying a combination of `aws:SourceAccount` and `aws:SourceArn` conditions \(both or one\)\. `aws:SourceAccount` is an AWS account ID of an owner of a hosted zone\. `aws:SourceArn` is an ARN of a hosted zone\.

The following are two examples of permissions you can add:

```
{
    "Sid": "Allow Route 53 DNSSEC Service",
    …
    "Resource": "*",
    "Condition": {
        "StringEquals": {
            "aws:SourceAccount": "111122223333"
        },
        "ArnEquals": {
            "aws:SourceArn": "arn:aws:route53:::hostedzone/HOSTED_ZONE_ID"
        }
    }
},
```

 \- Or \- 

```
{
    "Sid": "Allow Route 53 DNSSEC Service",
    …
    "Resource": "*",
    "Condition": {
        "StringEquals": {
            "aws:SourceAccount": ["1111-2222-3333","4444-5555-6666"]
        },
        "ArnLike": {
            "aws:SourceArn": "arn:aws:route53:::hostedzone/*"
        }
    }
},
```

For more information, see [The confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html) in the *IAM User Guide*\.

## Customer managed policy examples<a name="access-policy-examples-for-sdk-cli"></a>

You can create your own custom IAM policies to allow permissions for Route 53 actions\. You can attach these custom policies to the IAM groups that require the specified permissions\. These policies work when you are using the Route 53 API, the AWS SDKs, or the AWS CLI\. The following examples show permissions for several common use cases\. For the policy that grants a user full access to Route 53, see [Permissions required to use the Amazon Route 53 console](#console-required-permissions)\.

**Topics**
+ [Example 1: Allow read access to all hosted zones](#access-policy-example-allow-read-hosted-zones)
+ [Example 2: Allow creation and deletion of hosted zones](#access-policy-example-allow-create-delete-hosted-zones)
+ [Example 3: Allow full access to all domains \(public hosted zones only\)](#access-policy-example-allow-full-domain-access)
+ [Example 4: Allow creation of inbound and outbound Route 53 Resolver endpoints](#access-policy-example-create-resolver-endpoints)

### Example 1: Allow read access to all hosted zones<a name="access-policy-example-allow-read-hosted-zones"></a>

The following permissions policy grants the user permissions to list all hosted zones and view all the records in a hosted zone\.

```
{
    "Version": "2012-10-17",
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "route53:GetHostedZone", 
                "route53:ListResourceRecordSets"
            ],
            "Resource":"*"
        },
        {
            "Effect":"Allow",
            "Action":["route53:ListHostedZones"],
            "Resource":"*"
        }
    ]
}
```

### Example 2: Allow creation and deletion of hosted zones<a name="access-policy-example-allow-create-delete-hosted-zones"></a>

The following permissions policy allows users to create and delete hosted zones, and to track the progress of the change\. 

```
{
    "Version": "2012-10-17",
    "Statement":[
        {
            "Effect":"Allow",
            "Action":["route53:CreateHostedZone"],
            "Resource":"*"
        },
        {
            "Effect":"Allow",
            "Action":["route53:DeleteHostedZone"],
            "Resource":"*"
        },
        {
            "Effect":"Allow",
            "Action":["route53:GetChange"],
            "Resource":"*"
        }
    ]
}
```

### Example 3: Allow full access to all domains \(public hosted zones only\)<a name="access-policy-example-allow-full-domain-access"></a>

The following permissions policy allows users to perform all actions on domain registrations, including permissions to register domains and create hosted zones\. 

```
{
    "Version": "2012-10-17",
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "route53domains:*",
                "route53:CreateHostedZone"
            ],
            "Resource":"*"
        }
    ]
}
```

When you register a domain, a hosted zone is created at the same time, so a policy that includes permissions to register domains also requires permissions to create hosted zones\. \(For domain registration, Route 53 doesn't support granting permissions to individual resources\.\)

For information about permissions that are required to work with private hosted zones, see [Permissions required to use the Amazon Route 53 console](#console-required-permissions)\.

### Example 4: Allow creation of inbound and outbound Route 53 Resolver endpoints<a name="access-policy-example-create-resolver-endpoints"></a>

The following permissions policy allows users to use the Route 53 console to create Resolver inbound and outbound endpoints\. 

Some of these permissions are required only to create endpoints in the console\. You can omit these permissions if you want to grant permissions only to create inbound and outbound endpoints programmatically:
+ `route53resolver:ListResolverEndpoints` lets users see the list of inbound or outbound endpoints so they can verify that an endpoint was created\.
+ `DescribeAvailabilityZones` is required to display a list of Availability Zones\.
+ `DescribeVpcs` is required to display a list of VPCs\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "route53resolver:CreateResolverEndpoint",
                "route53resolver:ListResolverEndpoints",
                "ec2:CreateNetworkInterface",
                "ec2:DescribeAvailabilityZones",
                "ec2:DescribeNetworkInterfaces",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeSubnets",
                "ec2:DescribeVpcs"
            ],
            "Resource": "*"
        }
    ]
}
```