# Listing public hosted zones<a name="ListInfoOnHostedZone"></a>

You can use the Amazon Route 53 console to list all of the hosted zones that you created with the current AWS account\. For information about how to list hosted zones using the Route 53 API, see [ListHostedZones](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZones.html) in the *Amazon Route 53 API Reference*\. 

**To list the public hosted zones associated with an AWS account using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\. The page displays a list of the hosted zones that are associated with the AWS account that you are currently signed in with\.

1.  To filter hosted zones, use the search bar located at the top of the table\. 

   Search behavior depends on whether the hosted zone contains up to 2,000 records or more than 2,000 records:

   **Up to 2,000 hosted zones**
   + To display the records that have specific values, click the search bar, choose a property in the dropdown list, and enter a value\. You can also enter a value directly in the search bar and press Enter\. For example, to display the hosted zones that have a name beginning with **abc**, enter that value in the search bar and press Enter\.
   + To display only the hosted zones that have the same hosted zone type, select the type in the dropdown list, and enter the type\.

   **More than 2,000 hosted zones**
   + You can search for properties based on exact domain name, all properties, and type\.
   + Search using the exact domain name for faster search results\.