# Deleting a private hosted zone<a name="hosted-zone-private-deleting"></a>

This section explains how to delete a private hosted zone using the Amazon Route 53 console\.

You can delete a private hosted zone only if there are no records other than the default SOA and NS records\. If your hosted zone contains other records, you must delete them before you can delete your hosted zone\. This prevents you from accidentally deleting a hosted zone that still contains records\.

**Topics**
+ [Deleting private hosted zones that were created by another service](#delete-private-hosted-zone-created-by-another-service)
+ [Using the Route 53 console to delete a private hosted zone](#delete-private-hosted-zone-procedure)

## Deleting private hosted zones that were created by another service<a name="delete-private-hosted-zone-created-by-another-service"></a>

If a private hosted zone was created by another service, you can't delete it using the Route 53 console\. Instead, you need to use the applicable process for the other service:
+ **AWS Cloud Map** – To delete a hosted zone that AWS Cloud Map created when you created a private DNS namespace, delete the namespace\. AWS Cloud Map deletes the hosted zone automatically\. For more information, see [Deleting namespaces](https://docs.aws.amazon.com/cloud-map/latest/dg/deleting-namespaces.html) in the *AWS Cloud Map Developer Guide*\.
+ **Amazon Elastic Container Service \(Amazon ECS\) Service Discovery** – To delete a private hosted zone that Amazon ECS created when you created a service using service discovery, delete the Amazon ECS services that are using the namespace, and delete the namespace\. For more information, see [Deleting a service](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/delete-service.html) in the *Amazon Elastic Container Service Developer Guide*\.

## Using the Route 53 console to delete a private hosted zone<a name="delete-private-hosted-zone-procedure"></a>

To use the Route 53 console to delete a private hosted zone, perform the following procedure\.

**To delete a private hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Confirm that the hosted zone that you want to delete contains only an NS and an SOA record\. If it contains additional records, delete them:

   1. Choose the name of the hosted zone that you want to delete\.

   1. On the Record Sets page, if the list of records includes any records for which the value of the **Type** column is something other than **NS** or **SOA**, choose the row, and choose **Delete Record Set**\.

      To select multiple, consecutive records, choose the first row, press and hold the **Shift** key, and choose the last row\. To select multiple, non\-consecutive records, choose the first row, press and hold the **Ctrl** key, and choose the remaining rows\. 

   1. Choose **Back to Hosted Zones**\.

1. On the Hosted Zones page, choose the row for the hosted zone that you want to delete\.

1. Choose **Delete Hosted Zone**\.

1. Choose **Confirm**\.