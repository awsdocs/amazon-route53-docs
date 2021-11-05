# Updating or deleting health checks when DNS failover is configured<a name="health-checks-updating-deleting-tasks"></a>

When you want to update or delete health checks that are associated with records, or you want to change records that have associated health checks, you must consider how your changes affect routing of DNS queries and your DNS failover configuration\.

**Important**  
Route 53 doesn't prevent you from deleting a health check even if the health check is associated with one or more records\. If you delete a health check and you don't update the associated records, the future status of the health check can't be predicted and might change\. This will affect the routing of DNS queries for your DNS failover configuration\. 

To update or delete health checks that are already associated with records, we recommend that you perform the following tasks:

1. Identify the records that are associated with the health checks\. To identify the records that are associated with a health check, you must do one of the following: 
   + Review the records in each hosted zone using the Route 53 console\. For more information, see [Listing records](resource-record-sets-listing.md)\.
   + Run the `ListResourceRecordSets` API action on each hosted zone and review the response\. For more information, see [ListResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListResourceRecordSets.html) in the *Amazon Route 53 API Reference*\.

1. Assess the change in behavior that will result from updating or deleting health checks, or from updating records\. Based on that assessment, determine which changes to make\. 

   For more information, see [What happens when you omit health checks?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-omitting)

1. Change health checks and records as applicable\. For more information, see the following topics:
   + [Creating and updating health checks](health-checks-creating.md)
   + [Editing records](resource-record-sets-editing.md)

1. Delete the health checks that you're no longer using, if any\. For more information, see [Deleting health checks](health-checks-deleting.md)\. 