# Disabling DNSSEC signing<a name="dns-configuring-dnssec-disable"></a>

The steps for disabling DNSSEC signing in Route 53 vary, depending on the chain of trust that your hosted zone is part of\. 

For example, your hosted zone might have a parent zone that has a Delegation Signer \(DS\) record, as part of a chain of trust\. Your hosted zone might also be itself a parent zone for child zones that have enabled DNSSEC signing, which is another part of the chain of trust\. Investigate and determine the full chain of trust for your hosted zone before you take the steps to disable DNSSEC signing\.

The chain of trust for your hosted zone that enables DNSSEC signing must be carefully undone as you disable signing\. To remove your hosted zone from the chain of trust, you remove all DS records that are in place for the chain of trust that includes this hosted zone\. This means that you must do the following, in order:

1. Remove any DS records that this hosted zone has for child zones that are part of a chain of trust\.

1. Remove the DS record from the parent zone\. Skip this step if you have an island of trust \(there are no DS records in the parent zone and no DS records for child zones in this zone\)\. 

1. If you are not able to remove DS records, in order to remove the zone from the chain of trust, remove NS records from the parent zone\. For more information, see [Adding or changing name servers and glue records for a domain](domain-name-servers-glue-records.md)\.

The following incremental steps allow you to monitor the effectiveness of the individual steps to avoid DNS availability issues in your zone\.

**To disable DNSSEC signing**

1. Monitor zone availability\.

   You can monitor the zone for the availability of your domain names\. This can help you address any issues that might warrant rolling a step back after you enable DNSSEC signing\. You can monitor for your domain names with most traffic by using query logging\. For more information about setting up query logging, see [Monitoring Amazon Route 53](monitoring-overview.md)\.

   The monitoring can be done through a shell script, or through a paid service\. It shouldn't, however, be the only signal to determine if a rollback is required\. You might also get feedback from your customers due to a domain not being available\.

1. Find the current DS TTL\.

   You can find the DS TTL by running the following Unix command:

   `dig -t DS example.com example.com`

1. Find the maximum NS TTL\.

   There are 2 sets of NS records associated with your zones:
   + The delegation NS record — this is the NS record for your zone held by the parent zone\. You can find this by running the following Unix commands:

     First find the NS of your parent zone \(if your zone is example\.com, the parent zone is com\):

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

1. Remove the DS record from the parent zone\. 

   Contact the parent zone owner to remove the DS record\.

   **Rollback:** re\-insert the DS TTL, confirm DS insertion is effective, and wait for the maximum NS \(not DS\) TTL before all resolvers will start validating again\.

1. Confirm the DS removal is effective\.

   If the parent zone is on Route 53 DNS service, the parent zone owner can confirm full propagation through the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API\.

   Otherwise, you can periodically probe the parent zone for the DS record, and then wait another 10 minutes afterwards to increase the probability of the DS record removal being fully propagated\. Do note that some registrars have scheduled DS removal, for example once a day\.

1. Wait for the DS TTL\.

   Wait until all resolvers have expired the DS record from their caches\.

1. Disable DNSSEC signing and deactivate the key\-signing key \(KSK\)\.
   + [CLI](#CLI_dnssec_disable)
   + [Console](#console_dnssec_disable)

------
#### [ CLI ]

   Call [DisableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DisableHostedZoneDNSSEC.html) and [DeactivateKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeactivateKeySigningKey.html) APIs\.

   For example:

   ```
   aws --region us-east-1 route53 disable-hosted-zone-dnssec \
               --hosted-zone-id $hostedzone_id
   
   aws --region us-east-1 route53 deactivate-key-signing-key \
               --hosted-zone-id $hostedzone_id --name $ksk_name
   ```

------
#### [ Console ]

   **To disable DNSSEC signing**

   1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone that you want to disable DNSSEC signing for\.

   1. On the **DNSSEC signing** tab, choose **Disable DNSSEC signing**\.

   1. On the **Disable DNSSEC signing** page, choose one of the following options, depending on your scenario for the zone that you're disabling DNSSEC signing for\.
      + **Parent zone only** — This zone has a parent zone with a DS record\. In this scenario, you must remove the parent zone's DS record\.
      + **Child zones only** — This zone has a DS record for a chain of trust with one or more child zones\. In this scenario, you must remove the zone's DS records\.
      + **Parent and child zones** — This zone has both a DS record for a chain of trust with one or more child zones *and* a parent zone with a DS record\. In this scenario, do the following, in order:

        1. Remove the zone's DS records\.

        1. Remove the parent zone's DS record\.

        If you have an island of trust, you can skip this step\.

   1. Determine what the TTL is for each DS record that you remove in Step 4\.,Make sure that the longest TTL period has expired\.

   1. Select the check box to confirm that you have followed the steps in order\.

   1. Type *disable* in the field, as shown, and then choose **Disable**\.

   **To deactivate the key\-signing key \(KSK\)**

   1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, choose **Hosted zones**, and then choose a hosted zone that you want to deactivate the key\-signing key \(KSK\) for\.

   1. In the **Key\-signing keys \(KSKs\)** section, choose the KSK you want to deactivate, and under **Actions**, choose **Edit KSK**, set **KSK status** to **Inactive**, and then choose **Save KSK**\.

------

   **Rollback:** call [ActivateKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ActivateKeySigningKey.html) and [EnableHostedZoneDNSSEC](https://docs.aws.amazon.com/Route53/latest/APIReference/API_EnableHostedZoneDNSSEC.html) APIs\.

   For example:

   ```
   aws --region us-east-1 route53 activate-key-signing-key \
               --hosted-zone-id $hostedzone_id --name $ksk_name
   
   aws --region us-east-1 route53 enable-hosted-zone-dnssec \
               --hosted-zone-id $hostedzone_id
   ```

1. Confirm disabling zone signing is effective\.

   Use the Id from the `EnableHostedZoneDNSSEC()` call to run [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) to make sure that all Route 53 DNS Servers have stopped signing responses \(status = `INSYNC`\)\.

1. Observe name resolution\.

   You should observe that there are no issues resulting in resolvers validating your zone\. Allow 1\-2 weeks to also account for the time needed for your customers to report problems to you\.

1. \(Optional\) Clean up\.

   If you will not re\-enable signing, you can clean up the KSKs through [DeleteKeySigningKey](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteKeySigningKey.html) and delete the corresponding customer managed key to save costs\.