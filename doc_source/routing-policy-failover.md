# Failover routing<a name="routing-policy-failover"></a>

Failover routing lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy\. The primary and secondary records can route traffic to anything from an Amazon S3 bucket that is configured as a website to a complex tree of records\. For more information, see [Active\-passive failover](dns-failover-types.md#dns-failover-types-active-passive)\.

You can use failover routing policy for records in a private hosted zone\.

For information about values that you specify when you use the failover routing policy to create records, see the following topics:
+ [Values specific for failover records](resource-record-sets-values-failover.md)
+ [Values specific for failover alias records](resource-record-sets-values-failover-alias.md)
+ [Values that are common for all routing policies](resource-record-sets-values-shared.md)
+ [Values that are common for alias records for all routing policies](resource-record-sets-values-alias-common.md)