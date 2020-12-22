# Disabling DNSSEC signing<a name="dns-configuring-dnssec-disable"></a>

The steps for disabling DNSSEC signing in Route 53 vary, depending on the chain of trust that your hosted zone is part of\. 

For example, your hosted zone might have a parent zone that has a Delegation Signer \(DS\) record, as part of a chain of trust\. Your hosted zone might also be itself a parent zone for child zones that have enabled DNSSEC signing, which is another part of the chain of trust\. Investigate and determine the full chain of trust for your hosted zone before you take the steps to disable DNSSEC signing\.

The chain of trust for your hosted zone that enables DNSSEC signing must be carefully undone as you disable signing\. To remove your hosted zone from the chain of trust, you remove all DS records that are in place for the chain of trust that includes this hosted zone\. This means that you must do the following, in order:

1. Remove any DS records that this hosted zone has for child zones that are part of a chain of trust\.

1. Remove the DS record from the parent zone \(unless you have an island of trust\)\. 

These steps are called out in the procedure that follows\.

When you remove the DS records, you must wait until the longest TTL for the DS records that you remove has expired before you complete the step to disable DNSSEC signing\.

**Important**  
 If you disable DNSSEC signing for your hosted zone before the DNS changes have propagated, your domain could become unavailable on the internet\. Currently, the only way to verify that changes have propagated is to use the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) action\.

When you've determined where the relevant chain of trust DS records are for your hosted zone, follow the steps here to disable DNSSEC signing\. <a name="dns-configuring-dnssec-disable-procedure"></a>

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

     If you have an island of trust \(there are no DS records in the parent zone and no DS records for child zones in this zone\), you can skip this step\.

1. Determine what the TTL is for each DS record that you remove in Step 4, and before you continue, make sure that the longest TTL period has expired\.

1. Select the checkbox to confirm that you have followed the steps in order\.

1. Type *disable* in the field, as shown, and then choose **Disable**\.