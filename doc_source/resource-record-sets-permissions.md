# Resource record set permissions<a name="resource-record-sets-permissions"></a>

Resource record set permissions use Identity and Access management \(IAM\) policy conditions to allow you to set granular permissions for actions on the Route 53 console or for using the [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) API\.

A resource record set is defined as multiple resource records with the same name and type \(and class, but for most purposes the class is always IN, or internet\), but they contain different data\. For example, if you choose geolocation routing, you can have multiple A or AAAA records pointing to different endpoints for the same domain\. All of these A or AAAA records combine to form a resource record set\. For more information about DNS terminology, see [RFC 7719](https://datatracker.ietf.org/doc/html/rfc7719)\.

With the IAM policy conditions, `route53:ChangeResourceRecordSetsNormalizedRecordNames`, `route53:ChangeResourceRecordSetsRecordTypes`, and `route53:ChangeResourceRecordSetsActions`, you can grant granular administrative rights to other AWS users in any other AWS account\. This allows you to grant someone permissions to:
+ A single resource record set\.
+ All resource record sets of a specific DNS record type\.
+ Resource record sets where the names contain a specific string\.
+ Perform any, or all of the `CREATE | UPSERT | DELETE `actions when using the [ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) API, or the Route 53 console\.

You can also create access permissions that combine any of the Route 53 policy conditions\. For example, you can grant someone permissions to modify the A record data for marketing\-example\.com, but not allow that user to delete any records\. 

For more information about resource record set permissions, see [Using IAM policy conditions for fine\-grained access control to manage resource record sets](specifying-rrset-conditions.md)\.

To learn how to authenticate AWS users, see [Authenticating with identities](auth-and-access-control.md#security_iam_authentication) and to learn how to control access to Route 53 resources, see [Access control](auth-and-access-control.md#access-control)\.