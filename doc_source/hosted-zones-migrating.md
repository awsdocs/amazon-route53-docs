# Migrating a Hosted Zone to Another AWS Account<a name="hosted-zones-migrating"></a>

If you want to migrate a hosted zone from one AWS account to another, you can programmatically list the records in the old hosted zone, edit the output, and then programmatically create records in a new hosted zone using the edited output\. Note the following:

+ You can't migrate alias records that route traffic to traffic policy instances\.

+ You can use this process to create records in a new hosted zone that has a different name than an existing hosted zone but that has the same records\.

+ Some procedures use the AWS Command Line Interface \(AWS CLI\)\. You can also perform those procedures by using one of the AWS SDKs, the Amazon Route 53 API, or AWS Tools for Windows PowerShell\. We used the AWS CLI because it's easier for small numbers of hosted zones\.


+ [Step 1: Install or Upgrade the AWS CLI](#hosted-zones-migrating-install-cli)
+ [Step 2: Create the New Hosted Zone](#hosted-zones-migrating-create-hosted-zone)
+ [Step 3: Create a File That Contains the Records That You Want to Migrate](#hosted-zones-migrating-create-file)
+ [Step 4: Edit the Records That You Want to Migrate](#hosted-zones-migrating-edit-records)
+ [Step 5: Split Large Files into Smaller Files](#hosted-zones-migrating-split-file)
+ [Step 6: Create Records in the New Hosted Zone](#hosted-zones-migrating-create-records)
+ [Step 7: Compare Records in the Old and New Hosted Zones](#hosted-zones-migrating-compare)
+ [Step 8: Update the Domain to Use Name Servers for the New Hosted Zone](#hosted-zones-migrating-update-domain)

## Step 1: Install or Upgrade the AWS CLI<a name="hosted-zones-migrating-install-cli"></a>

For information about downloading, installing, and configuring the AWS CLI, see the [AWS Command Line Interface User Guide](http://docs.aws.amazon.com/cli/latest/userguide/)\.

**Note**  
Configure the CLI so you can use it when you're using both the account that created the hosted zone and the account that you're migrating the hosted zone to\. For more information, see [Configure](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) in the *AWS Command Line Interface User Guide*

If you're already using the AWS CLI, we recommend that you upgrade to the latest version of the CLI so the CLI commands support the latest Route 53 features\.

## Step 2: Create the New Hosted Zone<a name="hosted-zones-migrating-create-hosted-zone"></a>

The following procedure explains how to use the Route 53 console to create the hosted zone that you want to migrate to\.

**Note**  
Route 53 assigns a new set of four name servers to the new hosted zone\. After you migrate a hosted zone to another AWS account, you need to update the domain to use the name servers for the new hosted zone\. We remind you about this step later in the process\.

**To create the new hosted zone using a different account**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   Use the account that you want to migrate the hosted zone to\.

1. Create a hosted zone\. For more information, see [Creating a Public Hosted Zone](CreatingHostedZone.md)\.

1. Make note of the hosted zone ID\. In some cases, you'll need this information later in the process\.

1. Log out of the Route 53 console\.

## Step 3: Create a File That Contains the Records That You Want to Migrate<a name="hosted-zones-migrating-create-file"></a>

To migrate records from one hosted zone to another, you create a file that contains the records that you want to migrate, edit the file, and then use the edited file to create records in the new hosted zone\. Perform the following procedure to create the file\.

**To create a file that contains records that you want to migrate**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   Use the account that created the hosted zone that you want to migrate\.

1. Get the hosted zone ID for the hosted zone that you want to migrate:

   1. In the navigation pane, choose **Hosted zones**\.

   1. Find the hosted zone that you want to migrate\. If you have a lot of hosted zones, you can enter part of the name in the **Search all fields** field and press **Enter**\.

   1. Get the value of the **Hosted zone ID** column\.

1. Run the following command: 

   ```
   aws route53 list-resource-record-sets --hosted-zone-id hosted-zone-id > path-to-output-file
   ```

   Note the following:

   + For *hosted\-zone\-id*, specify the ID of the hosted zone that you got in step 2\. 

   + For *path\-to\-output\-file*, specify the directory path and file name that you want to save output in\. 

   + The `>` character sends output to the specified file\.

   + The AWS CLI automatically handles pagination for hosted zones that contain more than 100 records\. For more information, see [Using the AWS Command Line Interface's Pagination Options](http://docs.aws.amazon.com/cli/latest/userguide/pagination.html) in the *AWS Command Line Interface User Guide*\. 

     If you use another programmatic method to list records, such as one of the AWS SDKs, you can get a maximum of 100 records per page of results\. If the hosted zone contains more than 100 records, you must submit multiple requests to list all records\.

   For example, if you're running the AWS CLI on a Windows computer, you might run the following command:

   ```
   aws route53 list-resource-record-sets --hosted-zone-id ZOLDZONE12345 > c:\temp\list-records-ZOLDZONE12345.txt
   ```

1. Make a copy of this output\. After you create records in the new hosted zone, we recommend that you run the AWS CLI `list-resource-record-sets` command on the new hosted zone and compare the two outputs to ensure that all of the records were created\.

## Step 4: Edit the Records That You Want to Migrate<a name="hosted-zones-migrating-edit-records"></a>

The format of the file that you created in the previous procedure is close to the format that is required by the AWS CLI `change-resource-record-sets` command that you'll use to create records in the new hosted zone\. However, the file requires some edits\. Some of the changes must be applied to every record\. You can make these changes using the search and replace function in a good text editor\.

Open a copy of the file that you created in [Step 3: Create a File That Contains the Records That You Want to Migrate](#hosted-zones-migrating-create-file), and make the following changes:

+ Delete the first two lines at the top of the output:

  ```
  {
      "ResourceRecordSets": [
  ```

+ Delete the lines related to the NS and SOA records\. The new hosted zone will already have those records\.

+ *Optional* – Add a `Comment` element\.

+ Add a `Changes` element\.

+ For each record, add an `Action` and a `ResourceRecordSet` element\.

+ Add opening and closing braces \( `{ }` \) as required to make the JSON valid\.
**Note**  
You can use a JSON validator to verify that you have all of the braces and brackets in the correct places\. To find an online JSON validator, perform an internet search on "`json validator`"\.

+ If the hosted zone contains any aliases that refer to other records in the same hosted zone, make the following changes:

  + Change the hosted zone ID to the ID of the new hosted zone\.

  + Move the alias records to the bottom of the file\. Route 53 must create the record that an alias record refers to before it can create the alias record\.
**Important**  
If one or more alias records refer to other alias records, the records that are the alias target must appear in the file before the referencing alias records\. For example, if `alias.example.com` is the alias target for `alias.alias.example.com`, `alias.example.com` must appear first in the file\.

+ You can use this process to create records in a hosted zone that has a different name\. For every record in the output, change the domain name part of the `Name` element to the name of the new hosted zone\. For example, if you listed records in the example\.com hosted zone and you want to create records in an example\.net hosted zone, change the example\.com part of every record name to example\.net:

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

## Step 5: Split Large Files into Smaller Files<a name="hosted-zones-migrating-split-file"></a>

If you have a lot of records or if you have records that have a lot of values \(for example, a lot of IP addresses\), you might need to split the file into smaller files\. Here are the relevant limits:

+ Each file can contain a maximum of 1,000 records\.

+ The maximum combined length of the values in all `Value` elements is 32,000 bytes\.

## Step 6: Create Records in the New Hosted Zone<a name="hosted-zones-migrating-create-records"></a>

To create records in the new hosted zone, use the following AWS CLI command: 

```
aws route53 change-resource-record-sets --hosted-zone-id id-of-new-hosted-zone --change-batch file://path-to-file-that-contains-records
```

For example:

```
aws route53 change-resource-record-sets --hosted-zone-id ZNEWZONE1245 --change-batch file://c:/temp/change-records-ZNEWZONE1245.txt
```

## Step 7: Compare Records in the Old and New Hosted Zones<a name="hosted-zones-migrating-compare"></a>

We recommend that you list records in the new hosted zone and compare the output with the list of records from the old hosted zone to confirm that all records were created successfully in the new hosted zone\. Perform the following procedure:

**To compare records in the old and new hosted zones**

1. Run the following command:

   ```
   aws route53 list-resource-record-sets --hosted-zone-id hosted-zone-id > path-to-output-file
   ```

   Note the following:

   + For *hosted\-zone\-id*, specify the ID of the new hosted zone\. 

   + For *path\-to\-output\-file*, specify the directory path and file name that you want to save output in\. Specify a different name than you did in [Step 3: Create a File That Contains the Records That You Want to Migrate](#hosted-zones-migrating-create-file) so you have both files for a comparison\. 

   + The `>` character sends output to the specified file\.

   For example, if you're using a Windows computer, you might run the following command:

   ```
   aws route53 list-resource-record-sets --hosted-zone-id ZNEWZONE67890 > c:\temp\list-records-ZNEWZONE67890.txt
   ```

1. Compare the output with the output from [Step 3: Create a File That Contains the Records That You Want to Migrate](#hosted-zones-migrating-create-file)\.

   Other than the values of the NS and SOA records and any changes that you made in [Step 4: Edit the Records That You Want to Migrate](#hosted-zones-migrating-edit-records) \(such as different hosted zone IDs or domain names\), the two outputs should be identical\.

1. If the records in the new hosted zone don't match the records in the old hosted zone, you can do one of the following:

   + Make minor corrections using the Route 53 console\.

   + If a large number of records are missing, create a new text file that contains the missing records and then repeat [Step 6: Create Records in the New Hosted Zone](#hosted-zones-migrating-create-records)\.

   + Delete all the records except the NS and SOA records in the new hosted zone, and repeat the following steps:

     + [Step 4: Edit the Records That You Want to Migrate](#hosted-zones-migrating-edit-records)

     + [Step 5: Split Large Files into Smaller Files](#hosted-zones-migrating-split-file)

     + [Step 6: Create Records in the New Hosted Zone](#hosted-zones-migrating-create-records)

     + [Step 7: Compare Records in the Old and New Hosted Zones](#hosted-zones-migrating-compare)

## Step 8: Update the Domain to Use Name Servers for the New Hosted Zone<a name="hosted-zones-migrating-update-domain"></a>

When you're finished creating records in the new hosted zone, you can change the name servers for the domain to use the name servers for the new hosted zone\. For more information, see [Migrating DNS Service for an Existing Domain to Amazon Route 53Migrating DNS Service for an Existing Domain to Route 53](MigratingDNS.md)\.

**Note**  
Whether you use the process for a domain that's in use or the process for an inactive domain, you can skip the first three steps because you've already created a new hosted zone and the records in that hosted zone\.