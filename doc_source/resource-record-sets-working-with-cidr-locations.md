# Working with CIDR locations and blocks<a name="resource-record-sets-working-with-cidr-locations"></a>

<a name="CIDR-locations-work-with-procedure"></a>

**To work with CIDR locations by using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **IP\-based routing**, **CIDR collections** and then, in the **CIDR collections** section, click on a link to a CIDR collection in the **Collection name** list\.

   On the **CIDR locations** page, you can create a CIDR location, delete it, or edit a location and its blocks\.
   + To create a location, choose **Create CIDR location**\. 
   + In the **Create CIDR location** pane, enter a name for the location, the CIDR blocks associated with the location, and then choose **Create**\.
   + To view a CIDR location and the blocks within, choose the radio button next to a location to display its name and CIDR blocks in the location pane\.

     In this pane, you can also choose **Edit** to update the name of the location and/or its CIDR blocks\. Choose **Save** when you have finished editing\.
   + To delete a CIDR location and the blocks within, choose the radio button next to the location you want to delete, and then choose **Delete**\. To confirm deletion, enter the location name in the text input field and choose **Delete** again\.
**Important**  
Deleting a CIDR location can't be undone\. If you have any DNS records associated with the location, your domain might become unreachable\.