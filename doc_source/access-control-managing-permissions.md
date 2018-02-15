# Using Identity\-Based Policies \(IAM Policies\) for Amazon Route 53<a name="access-control-managing-permissions"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(users, groups, and roles\) and thereby grant permissions to perform operations on Amazon Route 53 resources\.

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options to manage access to your Route 53 resources\. For more information, see [Overview of Managing Access Permissions to Your Amazon Route 53 Resources](access-control-overview.md)\. 


+ [Permissions Required to Use the Amazon Route 53 Console](#console-required-permissions)
+ [AWS Managed \(Predefined\) Policies for Route 53](#access-policy-examples-aws-managed)
+ [Customer Managed Policy Examples](#access-policy-examples-for-sdk-cli)

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

For a list of actions and the ARN that you specify to grant or deny permission to use each action, see [Amazon Route 53 API Permissions: Actions, Resources, and Conditions Reference](r53-api-permissions-ref.md)\.

## Permissions Required to Use the Amazon Route 53 Console<a name="console-required-permissions"></a>

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
            "ec2:DescribeVpcs",
            "ec2:DescribeRegions",
            "sns:ListTopics",
            "sns:ListSubscriptionsByTopic",
            "sns:CreateTopic",
            "cloudwatch:DescribeAlarms",
            "cloudwatch:PutMetricAlarm",
            "cloudwatch:DeleteAlarms",
            "cloudwatch:GetMetricStatistics"
         ],
         "Resource":"*"
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

**`sns:ListTopics`, `sns:ListSubscriptionsByTopic`, `sns:CreateTopic`, `cloudwatch:DescribeAlarms`, `cloudwatch:PutMetricAlarm`, `cloudwatch:DeleteAlarms`**  
Let you create, delete, and view CloudWatch alarms\.

**`cloudwatch:GetMetricStatistics`**  
Lets you create CloudWatch metric health checks\.  
These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get statistics to display in the console\. 

## AWS Managed \(Predefined\) Policies for Route 53<a name="access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These AWS managed policies grant necessary permissions for common use cases so that you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. For Route 53, IAM provides four managed policies: 

+ **AmazonRoute53FullAccess** – Grants full access to Route 53 resources\.

+ **AmazonRoute53ReadOnlyAccess** – Grants read\-only access to Route 53 resources\.

+ **AmazonRoute53DomainsFullAccess** – Grants full access to Route 53 domain registration resources\.

+ **AmazonRoute53DomainsReadOnlyAccess** – Grants read\-only access to Route 53 domain registration resources\.

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies there\. You can also create your own custom IAM policies to allow permissions for Route 53 API operations\. You can attach these custom policies to the IAM users or groups that require those permissions\.

## Customer Managed Policy Examples<a name="access-policy-examples-for-sdk-cli"></a>

You can create your own custom IAM policies to allow permissions for Route 53 actions\. You can attach these custom policies to the IAM users or groups that require the specified permissions\. These policies work when you are using the Route 53 API, the AWS SDKs, or the AWS CLI\. The following examples show permissions for several common use cases\. For the policy that grants a user full access to Route 53, see [Permissions Required to Use the Amazon Route 53 Console](#console-required-permissions)\.


+ [Example 1: Allow Read Access to All Hosted Zones](#access-policy-example-allow-read-hosted-zones)
+ [Example 2: Allow Creation and Deletion of Hosted Zones](#access-policy-example-allow-create-delete-hosted-zones)
+ [Example 3: Allow Full Access to All Domains \(Public Hosted Zones Only\)](#access-policy-example-allow-full-domain-access)

### Example 1: Allow Read Access to All Hosted Zones<a name="access-policy-example-allow-read-hosted-zones"></a>

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

### Example 2: Allow Creation and Deletion of Hosted Zones<a name="access-policy-example-allow-create-delete-hosted-zones"></a>

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

### Example 3: Allow Full Access to All Domains \(Public Hosted Zones Only\)<a name="access-policy-example-allow-full-domain-access"></a>

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

For information about permissions that are required to work with private hosted zones, see [Permissions Required to Use the Amazon Route 53 Console](#console-required-permissions)\.