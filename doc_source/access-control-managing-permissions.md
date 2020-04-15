# Using identity\-based policies \(IAM policies\) for Amazon Route 53<a name="access-control-managing-permissions"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(users, groups, and roles\) and thereby grant permissions to perform operations on Amazon Route 53 resources\.

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options to manage access to your Route 53 resources\. For more information, see [Overview of managing access permissions to your Amazon Route 53 resources](access-control-overview.md)\. 

**Topics**
+ [Permissions required to use the Amazon Route 53 console](#console-required-permissions)
+ [AWS managed \(predefined\) policies for Route 53](#access-policy-examples-aws-managed)
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
                "s3:ListBucket",
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

**`s3:ListBucket`, `s3:GetBucketLocation`, and `s3:GetBucketWebsite`**  
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

## AWS managed \(predefined\) policies for Route 53<a name="access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These AWS managed policies grant necessary permissions for common use cases so that you can avoid having to investigate what permissions are needed\. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. For Route 53, IAM provides the following managed policies: 
+ **AmazonRoute53FullAccess** – Grants full access to Route 53 resources, including domain registration and health checking but excluding Route 53 Resolver
+ **AmazonRoute53ReadOnlyAccess** – Grants read\-only access to Route 53 resources, including domain registration and health checking but excluding Route 53 Resolver
+ **AmazonRoute53DomainsFullAccess** – Grants full access to Route 53 domain registration resources
+ **AmazonRoute53DomainsReadOnlyAccess** – Grants read\-only access to Route 53 domain registration resources
+ **AmazonRoute53ResolverFullAccess** – Grants full access to Resolver resources
+ **AmazonRoute53ResolverReadOnlyAccess** – Grants read\-only access to Resolver resources

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies there\. You can also create your own custom IAM policies to allow permissions for Route 53 API operations\. You can attach these custom policies to the IAM users or groups that require those permissions\.

## Customer managed policy examples<a name="access-policy-examples-for-sdk-cli"></a>

You can create your own custom IAM policies to allow permissions for Route 53 actions\. You can attach these custom policies to the IAM users or groups that require the specified permissions\. These policies work when you are using the Route 53 API, the AWS SDKs, or the AWS CLI\. The following examples show permissions for several common use cases\. For the policy that grants a user full access to Route 53, see [Permissions required to use the Amazon Route 53 console](#console-required-permissions)\.

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
                "ec2:CreateNetworkInterfacePermission",
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