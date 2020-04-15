# Routing traffic to Amazon WorkMail<a name="routing-to-workmail"></a>

If you're using Amazon WorkMail for your business email and you're using Amazon Route 53 as your DNS service, you can use Route 53 to route traffic to your Amazon WorkMail email domain\. The name of your Route 53 hosted zone \(such as example\.com\) must match the name of an Amazon WorkMail domain\.

**Note**  
You can route traffic to an Amazon WorkMail domain only for public hosted zones\.

To route traffic to Amazon WorkMail, perform the following four procedures\.<a name="routing-to-workmail-dns-procedure"></a>

**To configure Amazon Route 53 as your DNS service and add an Amazon WorkMail organization and email domain**

1. If you haven't registered the domain name that you want to use in your email addresses \(such as john@example\.com\), register the domain now so you know that the domain is available\. For more information, see [Registering a new domain](domain-register.md)\. 

   If Amazon Route 53 is not the DNS service for the email domain that you added to Amazon WorkMail, migrate DNS service for the domain to Route 53\. For more information, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

1. Add an Amazon WorkMail organization and email domain\. For more information, see [Getting started for new users](https://docs.aws.amazon.com/workmail/latest/adminguide/getting_started_new_user.html) in the *Amazon WorkMail Administrator Guide*\.<a name="routing-to-workmail-txt-procedure"></a>

**To create a Route 53 TXT record for Amazon WorkMail**

1. In the navigation pane of the Amazon WorkMail console, choose **Domains**\.

1. Choose the name of the email domain, such as example\.com, that you want to use to route traffic to Amazon WorkMail\.

1. Open another browser tab, and open the [Route 53 console](https://console.aws.amazon.com/route53/home)\.

1. In the Route 53 console, do the following:

   1. In the navigation pane, choose **Hosted Zones**\.

   1. Choose the name of the hosted zone that you want to use for your Amazon WorkMail email domain\.

1. In the Amazon WorkMail console, in the section **Step 1: Verify domain ownership**, go to the **Hostname** column, and copy the part of the value that precedes your email domain name\. 

   For example, if your Amazon WorkMail email domain is **example\.com** and the value of **Hostname** is **\_amazonses\.example\.com**, copy **\_amazonses**\.

1. In the Route 53 console, do the following:

   1. Choose **Create Record Set**\.

   1. For **Name**, paste the value that you copied in step 5\.

   1. For **Type**, choose **TXT – Text**\.

1. In the Amazon WorkMail console, for the TXT record, copy the value of the **Value** column, including the quotation marks\.

1. In the Route 53 console, do the following:

   1. For **Value**, paste the value that you copied in step 7\.

      Don't change any other settings\.

   1. Choose **Create**\.<a name="routing-to-workmail-mx-procedure"></a>

**To create a Route 53 MX record for Amazon WorkMail**

1. In the Amazon WorkMail console, in the section **Step 2: Finalize domain setup**, go to the row that has a **Record type** of **MX**, and copy the value of the **Value** column\.

1. In the Route 53 console, do the following:

   1. Choose **Create Record Set**\.

   1. For **Value**, paste the value that you copied in step 1\.

   1. For **Type**, choose **MX – Mail Exchange**\.

      Don't change any other settings\.

   1. Choose **Create**\.<a name="routing-to-workmail-cname-procedure"></a>

**To create four Route 53 CNAME records for Amazon WorkMail**

1. In the Amazon WorkMail console, in the section **Step 2: Finalize domain setup**, go to the first row that has a **Record type** of **CNAME**\. In the **Hostname** column, copy the part of the value that precedes your email domain name\.

   For example, if your Amazon WorkMail email domain is **example\.com** and the value of **Hostname** is **autodiscover\.example\.com**, copy **autodiscover**\.

1. In the Route 53 console, do the following:

   1. Choose **Create Record Set**\.

   1. For **Name**, paste the value that you copied in step 1\.

   1. For **Type**, choose **CNAME – Canonical Name**\.

1. In the Amazon WorkMail console, in the first row that has a **Record type** of **CNAME**, copy the value of the **Value** column\.

1. In the Route 53 console, do the following:

   1. For **Value**, paste the value that you copied in step 3\.

      Don't change any other settings\.

   1. Choose **Create**\.

1. Repeat steps 1 through 4 for the remaining CNAME records that are listed in the Amazon WorkMail console\.