# Enabling DNSSEC signing and establishing a chain of trust<a name="dns-configuring-dnssec-enable-signing"></a>

****  
The incremental steps apply to the hosted zone owner and the parent zone maintainer\. This can be the same person, but if not, the zone owner should notify and work with the parent zone maintainer\.

We recommend following the steps in this article to have your zone signed and included in the chain of trust\. The following steps will minimize the risk of onboarding onto DNSSEC\.

There are three steps to take to enable DNSSEC signing, as described in the following sections\. 

**Topics**
+ [Step 1: Prepare for enabling DNSSEC signing](#dns-configuring-dnssec-enable-signing-step-1)
+ [Step 2: Enable DNSSEC signing and create a KSK](#dns-configuring-dnssec-enable)
+ [Step 3: Establish chain of trust](#dns-configuring-dnssec-chain-of-trust)

## Step 1: Prepare for enabling DNSSEC signing<a name="dns-configuring-dnssec-enable-signing-step-1"></a>

The preparation steps help you minimize the risk of onboarding to DNSSEC by monitoring zone availability and lowering wait times between enabling signing and the insertion of the Delegation Signer \(DS\) record\.

**To prepare for enabling DNSSEC signing**

1. Monitor zone availability\.

   You can monitor the zone for the availability of your domain names\. This can help you address any issues that might warrant rolling a step back after you enable DNSSEC signing\. You can monitor for your domain names with most traffic by using query logging\. For more information about setting up query logging, see [Monitoring Amazon Route 53](monitoring-overview.md)\.

   The monitoring can be done through a shell script, or through a third party service\. It shouldn't, however, be the only signal to determine if a rollback is required\. You might also get feedback from your customers due to a domain not being available\.

1. Lower the zone's maximum TTL\.

   The zone’s maximum TTL is the longest TTL record in the zone\. In the following example zone, the zone’s maximum TTL is 1 day \(86400 seconds\)\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)

   Lowering the zone's maximum TTL will help reduce the wait time between enabling signing and the insertion of the Delegation Signer \(DS\) record\. We recommend lowering the zone's maximum TTL to 1 hour \(3600 seconds\)\. This allows you to roll back after only an hour if any resolver has problems with caching signed records\.

   **Rollback:** undo the TTL changes\.

1. Lower the SOA TTL and SOA minimum field\.

   The SOA minimum field is the last field in the SOA record data\. In the following example SOA record, the minimum field has the value of 5 minutes \(300 seconds\)\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-configuring-dnssec-enable-signing.html)

   The SOA TTL and SOA minimum field determines how long resolvers remember negative answers\. After you enable signing, Route 53 name servers start returning NSEC records for negative answers\. The NSEC contains information that resolvers might use to synthesize a negative answer\. If you have to roll back because the NSEC information caused a resolver to assume a negative answer for a name, then you only have to wait for the maximum of the SOA TTL and SOA minimum field for the resolver to stop the assumption\.

   **Rollback:** undo the SOA changes\.

1. Make sure the TTL and SOA minimum field changes are effective\.

   Use [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) to make sure your changes so far have been propagated to all Route 53 DNS servers\.

## Step 2: Enable DNSSEC signing and create a KSK<a name="dns-configuring-dnssec-enable"></a>

You can enable DNSSEC signing and create a key\-signing key \(KSK\) by using AWS CLI or on the Route 53 console\.
+ [CLI](#dnssec_CLI)
+ [Console](#dnssec_console)

When you provide or create a customer managed KMS key, there are several requirements\. For more information, see [Working with customer managed keys for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)\.

------
#### [ CLI ]

You can use a key that you already have, or create one by running an AWS CLI command like the following using your own values for `hostedzone_id`, `cmk_arn`, `ksk_name`, and `unique_string` \(to make the request unique\):

```
aws --region us-east-1 route53 create-key-signing-key \
			--hosted-zone-id $hostedzone_id \
			--key-management-service-arn $cmk_arn --name $ksk_name \
			--status ACTIVE \
			--caller-reference $unique_string
```

For more information about customer managed keys, see [Working with customer managed keys for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)\. See also [CreateKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateKeySigningKey.html)\.

To enable DNSSEC signing, run an AWS CLI command like the following, using your own value for the `hostedzone_id`:

```
aws --region us-east-1 route53 enable-hosted-zone-dnssec \
			--hosted-zone-id $hostedzone_id
```

For more information, see [enable\-hosted\-zone\-dnssec](https://docs.aws.amazon.com/cli/latest/reference/route53/enable-hosted-zone-dnssec.html) and [EnableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_EnableHostedZoneDNSSEC.html)\.

------
#### [ Console ]<a name="dns-configuring-dnssec-enable-procedure"></a>

**To enable DNSSEC signing and create a KSK**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone that you want to enable DNSSEC signing for\.

1. On the **DNSSEC signing** tab, choose **Enable DNSSEC signing**\.
**Note**  
If the option in this section is **Disable DNSSEC signing**, you have already completed the first step in enabling DNSSEC signing\. Be sure that you establish, or that there already exists, a chain of trust for the hosted zone for DNSSEC, and then you're done\. For more information, see [Step 3: Establish chain of trust](#dns-configuring-dnssec-chain-of-trust)\.

1. In the **Key\-signing key \(KSK\) creation** section, choose **Create new KSK**, and under **Provide KSK name**, enter a name for the KSK that Route 53 will create for you\. The name can include numbers, letters, and underscores \(\_\)\. It must be unique\.

1. Under **Customer managed CMK**, choose the customer managed key for Route 53 to use when it creates the KSK for you\. You can use an existing customer managed key that applies to DNSSEC signing, or create a new customer managed key\.

   When you provide or create a customer managed key, there are several requirements\. For more information, see [Working with customer managed keys for DNSSEC](dns-configuring-dnssec-cmk-requirements.md)\.

1. Enter the alias for an existing customer managed key\. If you want to use a new customer managed key, enter an alias for the customer managed key, and Route 53 will create one for you\.
**Note**  
If you choose to have Route 53 create a customer managed key, be aware that separate charges apply for each customer managed key\. For more information, see [AWS Key Management Service pricing](https://aws.amazon.com/kms/pricing/)\.

1. Choose **Enable DNSSEC signing**\.

------

**After you enable zone signing, complete the following steps** \(whether you used the console or the CLI\):

1. Ensure zone signing is effective\.

   Use the Id from the `EnableHostedZoneDNSSEC()` call to run [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) to make sure that all Route 53 DNS Servers are signing responses \(status = `INSYNC`\)\.

1. Wait for at least the previous zone’s maximum TTL\.

   Wait for resolvers to flush all unsigned records from their cache\. To achieve this you should wait for at least the previous zone’s maximum TTL\. In the `example.com` zone above, the wait time would be 1 day\.

1. Monitor for reports of customer issues\.

   After you have enabled zone signing, your customers might start seeing issues related to network devices and resolvers\. The recommended monitoring period is 2 weeks\.

   The following are examples of issues that you might see:
   + Some network devices can limit DNS response size to under 512 bytes, which is too small for some signed responses\. These network devices should be reconfigured to allow larger DNS response sizes\.
   + Some network devices do a deep inspection on DNS responses and strips certain records it doesn’t understand, like the ones used for DNSSEC\. These devices should be reconfigured\.
   + Some customers’ resolvers claim that they can accept a larger UDP response than their network supports\. You can test your network capability and configure your resolvers appropriately\. For more information see, [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest/)\.

**Rollback:** call [DisableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DisableHostedZoneDNSSEC.html) then rollback the steps in [Step 1: Prepare for enabling DNSSEC signing](#dns-configuring-dnssec-enable-signing-step-1)\.

## Step 3: Establish chain of trust<a name="dns-configuring-dnssec-chain-of-trust"></a>

After you enable DNSSEC signing for a hosted zone in Route 53, establish a chain of trust for the hosted zone to complete your DNSSEC signing setup\. You do this by creating a Delegation Signer \(DS\) record in the *parent* hosted zone, for your hosted zone, using the information that Route 53 provides\. Depending on where your domain is registered, you add the record to the parent hosted zone in Route 53 or at another domain registrar\.<a name="dns-configuring-dnssec-chain-of-trust-procedure"></a>

**To establish a chain of trust for DNSSEC signing**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone that you want to establish a DNSSEC chain of trust for\. *You must enable DNSSEC signing first\.*

1. On the **DNSSEC signing** tab, under **DNSSEC signing**, choose **View information to create DS record**\.
**Note**  
If you don't see **View information to create DS record** in this section, then you must enable DNSSEC signing before you establish the chain of trust\. Choose **Enable DNSSEC signing** and complete the steps as described in [Step 2: Enable DNSSEC signing and create a KSK](#dns-configuring-dnssec-enable), and then return to these steps to establish the chain of trust\.

1. Under **Establish a chain of trust**, choose either **Route 53 registrar** or **Another domain registrar**, depending on where your domain is registered\.

1. Use the provided values from step 3 to create a DS record for the parent hosted zone in Route 53\. If your domain is not hosted at Route 53, use the provided values to create a DS record at your domain registrar website\. 
   + If the parent zone is both registered and managed through Route 53, follow these steps:

     Make sure that you configure the correct signing algorithm \(ECDSAP256SHA256 and type 13\) and digest algorithm \(SHA\-256 and type 2\)\. 

     If Route 53 is your registrar, do the following in the Route 53 console:

     1. Note the **Key type**, **Signing algorithm**, and **Public key** values\. In the navigation pane, choose **Registered domains**\.

     1. Select a domain, and then, next to **DNSSEC status**, choose **Manage keys**\.

     1. In the **Manage DNSSEC keys** dialog box, choose the appropriate **Key type** and **Algorithm** for the **Route 53 registrar** from the dropdown menus\.

     1. Copy the **Public key** for the Route 53 registrar\. In the **Manage DNSSEC keys** dialog box, paste the value into the **Public key** box\.

     1. Choose **Add**\.

         Route 53 will add the DS record to the parent zone from the public key\. For example, if your domain is `example.com`, the DS record is added to the \.com DNS zone\.
   + If the parent zone is hosted on Route 53 or another registry, contact the parent zone owner to follow these instructions:

     To make sure the following steps go smoothly, introduce a low DS TTL to the parent zone\. We recommend setting the DS TTL to 5 minutes \(300 seconds\) for faster recovery if you need to roll your changes back\.
     + If your parent zone is administered by another registry, contact your registrar to introduce the DS record for your zone\. Typically you will not be able to adjust the TTL of the DS record\.
     + If your parent zone is hosted on Route 53, contact the parent zone owner to introduce the DS record for your zone\. 

       Provide the `$ds_record_value` to the parent zone owner\. You can get it by clicking on the **View Information to create DS record** in the console and copying the **DS record** field, or by calling [GetDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetDNSSEC.html) API and retrieving the value of the ‘DSRecord’ field:

       ```
       aws --region us-east-1 route53 get-dnssec 
                   --hosted-zone-id $hostedzone_id
       ```

       The parent zone owner can insert the record through the Route 53 console or CLI\.
       +  To insert the DS record by using AWS CLI, the parent zone owner creates and names a JSON file similar to the following example\. The parent zone owner might name the file something like `inserting_ds.json`\. 

         ```
         {
             "HostedZoneId": "$parent_zone_id",
             "ChangeBatch": {
                 "Comment": "Inserting DS for zone $zone_name",
                 "Changes": [
                     {
                         "Action": "UPSERT",
                         "ResourceRecordSet": {
                             "Name": "$zone_name",
                             "Type": "DS",
                             "TTL": 300,
                             "ResourceRecords": [
                                 {
                                     "Value": "$ds_record_value"
                                 }
                             ]
                         }
                     }
                 ]
             }
         }
         ```

         Then run the following command:

         ```
         aws --region us-east-1 route53 change-resource-record-sets 
                     --cli-input-json file://inserting_ds.json
         ```
       + To insert the DS record by using the console, 

         Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

         In the navigation pane, choose **Hosted zones**, the name of your hosted zone and then **Create record** button\. Make sure you choose Simple routing for the **Routing policy**\.

         In the **Record name** field enter the same name as the `$zone_name`, select DS fro the **Record type** drop\-down, and enter the value of `$ds_record_value` into the **Value** field, and choose **Create records**\.

   **Rollback:** remove the DS from the parent zone, wait for the DS TTL, and then roll back the steps for establishing trust\. If the parent zone is hosted on Route 53, the parent zone owner can change the `Action` from `UPSERT` to `DELETE` in the JSON file, and re\-run the example CLI above\.

1. Wait for the updates to propagate, based on the TTL for your domain records\.

   If the parent zone is on Route 53 DNS service, the parent zone owner can confirm full propagation through the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API\.

   Otherwise, you can periodically probe the parent zone for the DS record, and then wait another 10 minutes afterwards to increase the probability of the DS record insertion being fully propagated\. Do note that some registrars have scheduled DS insertion, for example, once a day\.

When you introduce the Delegation Signer \(DS\) record in the parent zone, the validated resolvers that have picked up the DS will start validating responses from the zone\.

To make sure the steps for establishing trust go smoothly, complete the following:

1. Find the maximum NS TTL\.

   There are 2 sets of NS records associated with your zones:
   + The delegation NS record — this is the NS record for your zone held by the parent zone\. You can find this by running the following Unix commands \(if your zone is example\.com, the parent zone is com\):

     `dig -t NS com`

     Pick one of the NS records and then run the following:

     `dig @one of the NS records of your parent zone -t NS example.com`

     For example:

     `dig @b.gtld-servers.net. -t NS example.com`
   + The in\-zone NS record — this is the NS record in your zone\. You can find this by running the following Unix command:

     `dig @one of the NS records of your zone -t NS example.com`

     For example:

     `dig @ns-0000.awsdns-00.co.uk. -t NS example.com`

     Note the maximum TTL for both zones\.

1. Wait for the maximum NS TTL\.

   Prior to the DS insertion, resolvers are getting a signed response, but aren't validating the signature\. When the DS record is inserted, resolvers will not see it until the NS record for the zone expires\. When resolvers re\-fetch the NS record, the DS record will then be also returned\.

   If your customer is running a resolver on a host with an out of sync clock, make sure the clock is within 1 hour of the correct time\.

   After completing this step, all DNSSEC\-aware resolvers will validate your zone\.

1. Observe name resolution\.

   You should observe that there are no issues with resolvers validating your zone\. Make sure you also account for the time needed for your customers to report problems to you\.

   We recommend monitoring for up to 2 weeks\.

1. \(Optional\) Lengthen the DS and NS TTLs\.

   If you are satisfied with the setup, you can save the TTL and SOA changes you made\. Note that Route 53 limits the TTL to 1 week for signed zones\. For more information, see [Configuring DNSSEC signing in Amazon Route 53](dns-configuring-dnssec.md)\.

   If you can change the DS TTL, we recommend that you set it to 1 hour\.