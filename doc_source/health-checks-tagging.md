# Naming and tagging health checks<a name="health-checks-tagging"></a>

You can add tags to Amazon Route 53 health checks, which lets you give each health check a name that is more comprehensible than the health check ID\. These are the same tags that AWS Billing and Cost Management provides for organizing your AWS bill\. For more information about using tags for cost allocation, see [Use cost allocation tags for custom billing reports](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/allocation.html) in the *AWS Billing and Cost Management User Guide*\. 

Each tag consists of a key \(the name of the tag\) and a value, both of which you define\. When you add tags to a health check, we recommend that you add one tag that has the following values for the key and value:
+ **key** – **Name**
+ **value** – The name that you want to give to the health check

The value of the **Name** tag appears in the list of health checks on the Route 53 console, which lets you readily distinguish health checks from one another\. To see other tags for a health check, you choose the health check and then choose the **Tags** tab\.

For more information about tags, see the following topics:
+ To add, edit, or delete the **Name** tag when you add or edit health checks in the Route 53 console, see [Creating, updating, and deleting health checks](health-checks-creating-deleting.md)\.
+ For an overview of tagging Route 53 resources, see [Tagging Amazon Route 53 resources](tagging-resources.md)\.

## Tag restrictions<a name="health-checks-tagging-restrictions"></a>

The following basic restrictions apply to tags:
+ Maximum number of tags per resource – 50
+ Maximum **Key** length – 128 Unicode characters
+ Maximum **Value** length – 256 Unicode characters
+ Valid values for **Key** and **Value** – uppercase and lowercase letters in the UTF\-8 character set, numbers, space, and the following characters: \_ \. : / = \+ \- and @
+ Tag keys and values are case sensitive
+ Don't use the `aws:` prefix for either keys or values; it's reserved for AWS use

## Adding, editing, and deleting tags for health checks<a name="health-checks-tagging-procedures"></a>

The following procedures show you how to use tags for your health checks on the Route 53 console\. 

*Topics*
+ [To add tags to health checks \(console\)](#health-checks-tagging-adding-procedure)
+ [To edit tags for health checks \(console\)](#health-checks-tagging-editing-procedure)
+ [To delete tags for health checks \(console\)](#health-checks-tagging-procedure)<a name="health-checks-tagging-adding-procedure"></a>

**To add tags to health checks \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. Select a health check, or select multiple health checks if you want to add the same tag to more than one health check\. 

1. In the bottom pane, choose the **Tags** tab, and then choose **Add/Edit Tags**\.

1. In the **Add/Edit Tags** dialog box, enter a name for the tag in the **Key** field, and enter a value in the **Value** field\.

1. Choose **Apply changes**\.<a name="health-checks-tagging-editing-procedure"></a>

**To edit tags for health checks \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. Select a health check\. 

   If you select multiple health checks that share the same tag, you cannot edit the value for all the tags simultaneously\. Note, however, that you can edit the value of a tag that appears in multiple health checks if you select health checks that have the tag and at least one than doesn't\.

   For example, suppose you select multiple health checks that have a **Cost Center** tag and one that doesn't\. You choose the option to add a tag, and you specify **Cost Center** for the key and **777** for the value\. For the selected health checks that already have a **Cost Center** tag, Route 53 changes the value to **777**\. For the one health check that doesn't have a **Cost Center** tag, Route 53 adds one and sets the value to **777**\.

1. In the bottom pane, choose the **Tags** tab, and then choose **Add/Edit Tags**\.

1. In the **Add/Edit Tags** dialog box, edit the value\.

1. Choose **Save**\.<a name="health-checks-tagging-procedure"></a>

**To delete tags for health checks \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. Select a health check, or select multiple health checks if you want to delete the same tag from more than one health check\. 

1. In the bottom pane, choose the **Tags** tab, and then choose **Add/Edit Tags**\.

1. In the **Add/Edit Tags** dialog box, choose the *X* next to the tag that you want to delete\.

1. Choose **Save**\.