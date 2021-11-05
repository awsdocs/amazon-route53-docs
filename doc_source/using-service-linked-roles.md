# Using Service\-Linked Roles for Amazon Route 53 Resolver<a name="using-service-linked-roles"></a>

Route 53 Resolver uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to Resolver\. Service\-linked roles are predefined by Resolver and include all the permissions that the service requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up Resolver easier because you don’t have to manually add the necessary permissions\. Resolver defines the permissions of its service\-linked roles, and unless defined otherwise, only Resolver can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting the related resources\. This protects your Resolver resources because you can't inadvertently remove permission to access the resources\.

For information about other services that support service\-linked roles, see [AWS Services that Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

**Topics**
+ [Service\-Linked Role Permissions for Resolver](#slr-permissions)
+ [Creating a Service\-Linked Role for Resolver](#create-slr)
+ [Editing a Service\-Linked Role for Resolver](#edit-slr)
+ [Deleting a Service\-Linked Role for Resolver](#delete-slr)
+ [Supported Regions for Resolver Service\-Linked Roles](#slr-regions)

## Service\-Linked Role Permissions for Resolver<a name="slr-permissions"></a>

Resolver uses the **`AWSServiceRoleForRoute53Resolver`** service\-linked role to deliver query logs on your behalf\.

The role permissions policy allows Resolver to complete the following actions on your resources:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "logs:CreateLogDelivery",
        "logs:GetLogDelivery",
        "logs:UpdateLogDelivery",
        "logs:DeleteLogDelivery",
        "logs:ListLogDeliveries",
        "logs:DescribeResourcePolicies",
        "logs:DescribeLogGroups",
        "s3:GetBucketPolicy"
      ],
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}
```

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a Service\-Linked Role for Resolver<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When you create a resolver query log configuration association in the Amazon Route 53 console, the AWS CLI, or the AWS API, Resolver creates the service\-linked role for you\. 

**Important**  
This service\-linked role can appear in your account if you completed an action in another service that uses the features supported by this role\. Also, if you were using the Resolver service before August 12, 2020, when it began supporting service\-linked roles, then Resolver created the `AWSServiceRoleForRoute53Resolver` role in your account\. To learn more, see [A New Role Appeared in My IAM Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html#troubleshoot_roles_new-role-appeared)\.

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you create a new Resolver query log configuration association, the `AWSServiceRoleForRoute53Resolver` service\-linked role is created for you again\. 

## Editing a Service\-Linked Role for Resolver<a name="edit-slr"></a>

Resolver does not allow you to edit the `AWSServiceRoleForRoute53Resolver` service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a Service\-Linked Role for Resolver<a name="delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\.

**Note**  
If the Resolver service is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To delete Resolver resources used by the `AWSServiceRoleForRoute53Resolver`**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Expand the Route 53 console menu\. In the upper left corner of the console, choose the three horizontal bars \(![\[Menu icon\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/menu-icon.png)\) icon\.

1. Within the **Resolver **menu, choose **Query logging**\.

1. Select the check box next to the name of your query logging configuration, and then choose **Delete**\.

1. In the **Delete query logging configuration** text box, select **Stop logging queries**\.

   This will disassociate the configuration from the VPC\. You can also disassociate the query logging configuration programmatically\. For more information, see [disassociate\-resolver\-query\-log\-config](https://docs.aws.amazon.com/cli/latest/reference/route53resolver/disassociate-resolver-query-log-config.html)\.

1. After logging queries has stopped, you can optionally type **delete** in the field and choose **Delete** to delete the query logging configuration\. However, this is not necessary for deleting the resources used by `AWSServiceRoleForRoute53Resolver`\.

**To manually delete the service\-linked role using IAM**

Use the IAM console, the AWS CLI, or the AWS API to delete the `AWSServiceRoleForRoute53Resolver` service\-linked role\. For more information, see [Deleting a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported Regions for Resolver Service\-Linked Roles<a name="slr-regions"></a>

Resolver does not support using service\-linked roles in every Region where the service is available\. You can use the `AWSServiceRoleForRoute53Resolver` role in the following Regions\.


****  

| Region name | Region identity | Support in Resolver | 
| --- | --- | --- | 
| US East \(N\. Virginia\) | us\-east\-1 | Yes | 
| US East \(Ohio\) | us\-east\-2 | Yes | 
| US West \(N\. California\) | us\-west\-1 | Yes | 
| US West \(Oregon\) | us\-west\-2 | Yes | 
| Asia Pacific \(Mumbai\) | ap\-south\-1 | Yes | 
| Asia Pacific \(Osaka\) | ap\-northeast\-3 | Yes | 
| Asia Pacific \(Seoul\) | ap\-northeast\-2 | Yes | 
| Asia Pacific \(Singapore\) | ap\-southeast\-1 | Yes | 
| Asia Pacific \(Sydney\) | ap\-southeast\-2 | Yes | 
| Asia Pacific \(Tokyo\) | ap\-northeast\-1 | Yes | 
| Canada \(Central\) | ca\-central\-1 | Yes | 
| Europe \(Frankfurt\) | eu\-central\-1 | Yes | 
| Europe \(Ireland\) | eu\-west\-1 | Yes | 
| Europe \(London\) | eu\-west\-2 | Yes | 
| Europe \(Paris\) | eu\-west\-3 | Yes | 
| South America \(São Paulo\) | sa\-east\-1 | Yes | 
| China \(Beijing\) | cn\-north\-1 | Yes | 
| China \(Ningxia\) | cn\-northwest\-1 | Yes | 
| AWS GovCloud \(US\) | us\-gov\-east\-1 | Yes | 
| AWS GovCloud \(US\) | us\-gov\-west\-1 | Yes | 