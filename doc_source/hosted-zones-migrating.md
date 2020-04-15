# Migrating a hosted zone to a different AWS account<a name="hosted-zones-migrating"></a>

If you want to migrate a hosted zone from one AWS account to a different account, you can programmatically list the records in the old hosted zone, edit the output, and then programmatically create records in a new hosted zone using the edited output\. Note the following:
+ If you have only a few records, you can also use the Route 53 console to create records in the new hosted zone\. For more information, see [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)\.
+ Some procedures use the AWS Command Line Interface \(AWS CLI\)\. You can also perform those procedures by using one of the AWS SDKs, the Amazon Route 53 API, or AWS Tools for Windows PowerShell\. For this topic, we use the AWS CLI because it's easier for small numbers of hosted zones\.
+ You can also use this process to create records in a new hosted zone that has a different name than an existing hosted zone but that has the same records\.
+ You can't migrate alias records that route traffic to traffic policy instances\.

**Topics**
+ [Step 1: Install or upgrade the AWS CLI](#hosted-zones-migrating-install-cli)
+ [Step 2: Create the new hosted zone](#hosted-zones-migrating-create-hosted-zone)
+ [Step 3: Create a file that contains the records that you want to migrate](#hosted-zones-migrating-create-file)
+ [Step 4: Edit the records that you want to migrate](#hosted-zones-migrating-edit-records)
+ [Step 5: Split large files into smaller files](#hosted-zones-migrating-split-file)
+ [Step 6: Create records in the new hosted zone](#hosted-zones-migrating-create-records)
+ [Step 7: Compare records in the old and new hosted zones](#hosted-zones-migrating-compare)
+ [Step 8: Update the domain registration to use name servers for the new hosted zone](#hosted-zones-migrating-update-domain)
+ [Step 9: Wait for DNS resolvers to start using the new hosted zone](#hosted-zones-migrating-wait-for-ttl)
+ [Step 10: \(Optional\) delete the old hosted zone](#hosted-zones-migrating-delete-old-hosted-zone)

## Step 1: Install or upgrade the AWS CLI<a name="hosted-zones-migrating-install-cli"></a>

For information about downloading, installing, and configuring the AWS CLI, see the [AWS Command Line Interface User Guide](https://docs.aws.amazon.com/cli/latest/userguide/)\.

**Note**  
Configure the CLI so that you can use it when you're using both the account that created the hosted zone and the account that you're migrating the hosted zone to\. For more information, see [Configure](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) in the *AWS Command Line Interface User Guide*

If you're already using the AWS CLI, we recommend that you upgrade to the latest version of the CLI so that the CLI commands support the latest Route 53 features\.

## Step 2: Create the new hosted zone<a name="hosted-zones-migrating-create-hosted-zone"></a>

The following procedure explains how to use the Route 53 console to create the hosted zone that you want to migrate to\.

**Note**  
Route 53 assigns a new set of four name servers to the new hosted zone\. After you migrate a hosted zone to another AWS account, you need to update the domain registration to use the name servers for the new hosted zone\. We remind you about this step later in the process\.<a name="hosted-zones-migrating-create-hosted-zone-procedure"></a>

**To create the new hosted zone using a different account**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   Sign in with the account credentials for the account that you want to migrate the hosted zone to\.

1. Create a hosted zone\. For more information, see [Creating a public hosted zone](CreatingHostedZone.md)\.

1. Make note of the hosted zone ID\. In some cases, you'll need this information later in the process\.

1. Log out of the Route 53 console\.

## Step 3: Create a file that contains the records that you want to migrate<a name="hosted-zones-migrating-create-file"></a>

To migrate records from one hosted zone to another, you create a file that contains the records that you want to migrate, edit the file, and then use the edited file to create records in the new hosted zone\. Perform the following procedure to create the file\.<a name="hosted-zones-migrating-create-file-procedure"></a>

**To create a file that contains records that you want to migrate**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   Sign in with the account credentials for the account that created the hosted zone that you want to migrate\.

1. Get the hosted zone ID for the hosted zone that you want to migrate:

   1. In the navigation pane, choose **Hosted zones**\.

   1. Find the hosted zone that you want to migrate\. If you have a lot of hosted zones, you can enter part of the name in the **Search all fields** field and press **Enter** to filter the list\.

   1. Get the value of the **Hosted zone ID** column\.

1. Run the following command: 

   ```
   aws route53 list-resource-record-sets --hosted-zone-id hosted-zone-id > path-to-output-file
   ```

   Note the following:
   + For *hosted\-zone\-id*, specify the ID of the hosted zone that you got in step 2 of this procedure\. 
   + For *path\-to\-output\-file*, specify the directory path and file name that you want to save the output in\. 
   + The `>` character sends the output to the specified file\.
   + The AWS CLI automatically handles pagination for hosted zones that contain more than 100 records\. For more information, see [Using the AWS Command Line Interface's pagination options](https://docs.aws.amazon.com/cli/latest/userguide/pagination.html) in the *AWS Command Line Interface User Guide*\. 

     If you use another programmatic method to list records, such as one of the AWS SDKs, you can get a maximum of 100 records per page of results\. If the hosted zone contains more than 100 records, you must submit multiple requests to list all records\.
   + To run the command in versions of Windows PowerShell earlier than 6\.0, use the following syntax:

     ```
     aws route53 list-resource-record-sets --hosted-zone-id hosted-zone-id | Out-File path-to-output-file -Encoding utf8
     ```

   For example, if you're running the AWS CLI on a Windows computer, you might run the following command:

   ```
   aws route53 list-resource-record-sets --hosted-zone-id ZOLDZONE12345 > c:\temp\list-records-ZOLDZONE12345.txt
   ```

   If you're running the AWS CLI on a Windows computer in a version of Windows PowerShell earlier than 6\.0, you might run the following command:

   ```
   aws route53 list-resource-record-sets --hosted-zone-id ZOLDZONE12345 | Out-File c:\temp\list-records-ZOLDZONE12345.txt -Encoding utf8
   ```

1. Make a copy of this output\. After you create records in the new hosted zone, we recommend that you run the AWS CLI `list-resource-record-sets` command on the new hosted zone and compare the two outputs to ensure that all the records were created\.

## Step 4: Edit the records that you want to migrate<a name="hosted-zones-migrating-edit-records"></a>

The format of the file that you created in the previous procedure is close to the format that is required by the AWS CLI `change-resource-record-sets` command that you use to create records in the new hosted zone\. However, the file requires some edits\. You must apply some of the changes to every record\. You can make these changes using the search and replace function in a good text editor\.

Open a copy of the file that you created in [Step 3: Create a file that contains the records that you want to migrate](#hosted-zones-migrating-create-file), and make the following changes:
+ Delete the first two lines at the top of the output:

  ```
  {
      "ResourceRecordSets": [
  ```
+ Delete the lines related to the NS and SOA records\. The new hosted zone already has those records\.
+ *Optional* – Add a `Comment` element\.
+ Add a `Changes` element\.
+ For each record, add an `Action` and a `ResourceRecordSet` element\.
+ Add opening and closing braces \( `{ }` \) as required to make the JSON code valid\.
**Note**  
You can use a JSON validator to verify that you have all the braces and brackets in the correct places\. To find an online JSON validator, do an internet search on "`json validator`"\.
+ If the hosted zone contains any aliases that refer to other records in the same hosted zone, make the following changes:
  + Change the hosted zone ID to the ID of the new hosted zone\.
  + Move the alias records to the bottom of the file\. Route 53 must create the record that an alias record refers to before it can create the alias record\.
**Important**  
If one or more alias records refer to other alias records, the records that are the alias target must appear in the file before the referencing alias records\. For example, if `alias.example.com` is the alias target for `alias.alias.example.com`, `alias.example.com` must appear first in the file\.
  + Delete any alias records that route traffic to a traffic policy instance\. Make note of the records so you can recreate them later\.
+ You can use this process to create records in a hosted zone that has a different name\. For every record in the output, change the domain name part of the `Name` element to the name of the new hosted zone\. For example, if you list records in the example\.com hosted zone and you want to create records in an example\.net hosted zone, change the example\.com part of every record name to example\.net:

  From:
  + `"Name": "example.com."`
  + `"Name": "www.example.com."`

  To:
  + `"Name": "example.net."`
  + `"Name": "www.example.net."`

The following example shows the edited version of records for a hosted zone for example\.com\. The red, italicized text is new:

```
{
    "Comment": "string",
    "Changes": [
        {
            "Action": "CREATE",
            "ResourceRecordSet":{
                "ResourceRecords": [
                    {
                        "Value": "192.0.2.4"
                    }, 
                    {
                        "Value": "192.0.2.5"
                    }, 
                    {
                        "Value": "192.0.2.6"
                    }
                ], 
                "Type": "A", 
                "Name": "route53documentation.com.", 
                "TTL": 300
            }
        },
        {
            "Action": "CREATE",
            "ResourceRecordSet":{
                "AliasTarget": {
                    "HostedZoneId": "Z3BJ6K6RIION7M",
                    "EvaluateTargetHealth": false,
                    "DNSName": "s3-website-us-west-2.amazonaws.com."
            },
                "Type": "A",
                "Name": "www.route53documentation.com."
            }
        }
    ]
}
```

## Step 5: Split large files into smaller files<a name="hosted-zones-migrating-split-file"></a>

If you have a lot of records or if you have records that have a lot of values \(for example, a lot of IP addresses\), you might need to split the file into smaller files\. Here are the maximums:
+ Each file can contain a maximum of 1,000 records\.
+ The maximum combined length of the values in all `Value` elements is 32,000 bytes\.

## Step 6: Create records in the new hosted zone<a name="hosted-zones-migrating-create-records"></a>

To create records in the new hosted zone, use the following AWS CLI command: 

```
aws route53 change-resource-record-sets --hosted-zone-id id-of-new-hosted-zone --change-batch file://path-to-file-that-contains-records
```

For example:

```
aws route53 change-resource-record-sets --hosted-zone-id ZNEWZONE1245 --change-batch file://c:/temp/change-records-ZNEWZONE1245.txt
```

If you deleted any alias records that route traffic to a traffic policy instance, recreate them using the Route 53 console\. For more information, see [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)\.

## Step 7: Compare records in the old and new hosted zones<a name="hosted-zones-migrating-compare"></a>

To confirm that you successfully created all of your records in the new hosted zone, we recommend that you list the records in the new hosted zone and compare the output with the list of records from the old hosted zone\. To do that, perform the following procedure\.<a name="hosted-zones-migrating-compare-procedure"></a>

**To compare records in the old and new hosted zones**

1. Run the following command:

   ```
   aws route53 list-resource-record-sets --hosted-zone-id hosted-zone-id > path-to-output-file
   ```

   Specify the following values:
   + For *hosted\-zone\-id*, specify the ID of the new hosted zone\. 
   + For *path\-to\-output\-file*, specify the directory path and file name that you want to save the output in\. Use a file name that is different from the file name that you used in [Step 3: Create a file that contains the records that you want to migrate](#hosted-zones-migrating-create-file)\. Using a different file name ensures that the new file doesn't overwrite the old file\. 
   + The `>` character sends output to the specified file\.

   For example, if you're using a Windows computer, you might run the following command:

   ```
   aws route53 list-resource-record-sets --hosted-zone-id ZNEWZONE67890 > c:\temp\list-records-ZNEWZONE67890.txt
   ```

1. Compare the output with the output from [Step 3: Create a file that contains the records that you want to migrate](#hosted-zones-migrating-create-file)\.

   Other than the values of the NS and SOA records and any changes that you made in [Step 4: Edit the records that you want to migrate](#hosted-zones-migrating-edit-records) \(such as different hosted zone IDs or domain names\), the two outputs should be identical\.

1. If the records in the new hosted zone don't match the records in the old hosted zone, you can do one of the following:
   + Make minor corrections using the Route 53 console\. For more information, see [Editing records](resource-record-sets-editing.md)\.
   + If a large number of records are missing, create a new text file that contains the missing records and then repeat [Step 6: Create records in the new hosted zone](#hosted-zones-migrating-create-records)\.
   + Delete all the records except the NS and SOA records in the new hosted zone, and repeat the following steps:
     + [Step 4: Edit the records that you want to migrate](#hosted-zones-migrating-edit-records)
     + [Step 5: Split large files into smaller files](#hosted-zones-migrating-split-file)
     + [Step 6: Create records in the new hosted zone](#hosted-zones-migrating-create-records)
     + [Step 7: Compare records in the old and new hosted zones](#hosted-zones-migrating-compare)

## Step 8: Update the domain registration to use name servers for the new hosted zone<a name="hosted-zones-migrating-update-domain"></a>

When you finish creating records in the new hosted zone, change the name servers for the domain registration to use the name servers for the new hosted zone\.

**Important**  
If you don't update the domain registration to use the name servers for the new hosted zone, Route 53 will continue to use the old hosted zone to route traffic for the domain\. If you delete the old hosted zone without updating name servers for the domain registration, the domain will become unavailable on the internet\. If you add, update, or delete records in the new hosted zone without updating name servers for the domain registration, then traffic won't be routed based on those changes\.

For more information, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

**Note**  
Whether you use the process to migrate DNS service for a domain that's in use or the process for an inactive domain, you can skip the following steps because you've already created a new hosted zone and the records in that hosted zone:  
Step 1: Get Your Current DNS Configuration from the Current DNS Service Provider
Step 2: Create a Hosted Zone
Step 3: Create Records

## Step 9: Wait for DNS resolvers to start using the new hosted zone<a name="hosted-zones-migrating-wait-for-ttl"></a>

If your domain is in use—for example, if your users are using the domain name to browse to a website or access a web application—then DNS resolvers have cached the names of the name servers that were provided by your current DNS service provider\. A DNS resolver that cached that information a few minutes ago will save it for up to two days\.

**Note**  
If you created any records in the new hosted zone that don't appear in the old hosted zone, your users can't use the new records to access your resources until resolvers start using the name servers for the new hosted zone\. For example, suppose you create a record, test\.example\.com, in the new hosted zone that should route internet traffic to your website\. If the record doesn't appear in the old hosted zone, you can't enter test\.example\.com in a web browser until resolvers start using the new hosted zone\.

To ensure that migrating a hosted zone to another AWS account has completed before you delete the old hosted zone, wait for two days after you update the domain registration to use name servers for the new hosted zone\. After the two\-day TTL expires and resolvers request the name servers for your domain, the resolvers will get the current name servers\.

## Step 10: \(Optional\) delete the old hosted zone<a name="hosted-zones-migrating-delete-old-hosted-zone"></a>

When you're confident that you don't need the old hosted zone any longer, you can optionally delete it\.

**Important**  
Don't delete the old hosted zone or any records in that hosted zone for at least 48 hours after you update the domain registration to use name servers for the new hosted zone\. If you delete the old hosted zone before DNS resolvers stop using the records in that hosted zone, your domain could be unavailable on the internet until resolvers start using the new hosted zone\.

The hosted zone must be empty except for the default NS and SOA records\. If the old hosted zone contains a lot of records, deleting them using the console can take a long time\. One option is to perform the following steps:

1. Make another copy of the edited file from [Step 4: Edit the records that you want to migrate](#hosted-zones-migrating-edit-records)\.

1. In the copy of the file, change `"Action": "CREATE"` to `"Action": "DELETE"` for every record\.

1. Use the following AWS CLI command to delete the records:

   ```
   aws route53 change-resource-record-sets --hosted-zone-id id-of-old-hosted-zone --change-batch file://path-to-file-that-contains-records
   ```
**Important**  
Make sure that the value that you specify for the hosted zone ID is the ID of the old hosted zone, not the ID of the new hosted zone\.

1. Delete any remaining records and the hosted zone:

   1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

      Sign in with the account credentials for the account that created the old hosted zone\.

   1. In the navigation pane, choose **Hosted zones**\.

   1. Choose the name of the old hosted zone\. If you have a lot of hosted zones, you can enter part of the name in the **Search all fields** field and press **Enter** to filter the list\.

   1. If the hosted zone contains any records other than the default NS and SOA records \(such as alias records that route traffic to a traffic policy instance\), choose the corresponding check boxes and choose **Delete Record Set**\.

   1. Choose **Back to Hosted Zones**\.

   1. In the list of hosted zones, choose the radio button for the hosted zone that you want to delete\.

   1. Choose **Delete Hosted Zone**\.