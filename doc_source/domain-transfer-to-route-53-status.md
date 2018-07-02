# Viewing the Status of a Domain Transfer<a name="domain-transfer-to-route-53-status"></a>

After you initiate the transfer of a domain from another domain registrar to Amazon Route 53, you can track the status on the **Registered Domains** page of the Route 53 console\. The **Status** column includes a brief description of the current step\. The following list includes the text in the console and a more detailed description of each step\.

**Note**  
When you submit a transfer request, the initial status is **Domain transfer request submitted**, which indicates that we've received your request\.

**Determining whether the domain meets transfer requirements \(step 1 of 14\)**  
We're confirming that your domain's status is eligible for transfer\. You must unlock your domain, and the domain can't have any of the following status codes when you submit the transfer request:   

+ clientTransferProhibited

+ pendingDelete

+ pendingTransfer

+ redemptionPeriod

**Verifying WHOIS information \(step 2 of 14\)**  
We sent a WHOIS query for your domain to determine whether you've disabled the privacy protection for the domain\. If privacy protection is still enabled with your current registrar, we won't be able to access the information we need to transfer the domain\.  
If the current registrar for the domain won't let you turn off privacy protection, we can still transfer the domain if you specified a valid authorization code in [Step 5: Request the Transfer](domain-transfer-to-route-53.md#domain-transfer-to-route-53-request-transfer)\.

**Sent email to registrant contact to get transfer authorization \(step 3 of 14\)**  
We've sent an email to the registrant contact for the domain to confirm that the transfer was requested by an authorized contact of the domain\.

**Verifying transfer with current registrar \(step 4 of 14\)**  
We've sent a request to the current registrar for the domain to initiate the transfer\.

**Awaiting authorization from registrant contact \(step 5 of 14\)**  
We sent email to the registrant contact for the domain \(see step 3 of 14\), and we're waiting for the registrant contact to click a link in the email to authorize the transfer\. If you didn't receive the email for some reason, see [Resending Authorization and Confirmation Emails](domain-click-email-link.md)\.

**Contacted current registrar to request transfer \(step 6 of 14\)**  
We're working with the current registrar for the domain to finalize the transfer\.

**Waiting for the current registrar to complete the transfer \(step 7 of 14\)**  
Your current registrar is confirming that your domain meets the requirements for being transferred\. This step might take up to ten days, depending on the TLD for your domain:  

+ [Generic Top\-Level Domains](registrar-tld-list.md#registrar-tld-list-generic) – take up to seven days

+ [Geographic Top\-Level Domains](registrar-tld-list.md#registrar-tld-list-geographic) \(also known as country code top\-level domains\) – take up to ten days
For most registrars, the process is entirely automated and can't be accelerated\. Some registrars send you an email that asks you to approve the transfer; if your registrar sends this confirmation email, the transfer process might be much faster than seven to ten days\.  
For information about reasons that a registrar might reject the transfer, see [Transfer Requirements for Top\-Level Domains](domain-transfer-to-route-53.md#domain-transfer-to-route-53-requirements)\.

**Confirming with the registrant contact that the contact initiated the transfer \(step 8 of 14\)**  
Some TLD registries send the registrant contact another email to confirm that the domain transfer was requested by an authorized user\.

**Synchronizing name servers with the registry \(step 9 of 14\)**  
This step occurs only if the name servers that you provided as part of the transfer request are different from the name servers that are listed with the current registrar\. We'll try to update your name servers to the new name servers that you provided\.

**Synchronizing settings with the registry \(step 10 of 14\)**  
We're verifying that the transfer has completed successfully, and we're synchronizing your domain\-related data with our registrar associate\.

**Sending updated contact information to the registry \(step 11 of 14\)**  
If you changed the ownership of the domain when you requested the transfer, we're trying to make this change\. However, most registries don't allow a transfer of ownership as part of the domain transfer process\.

**Finalizing the transfer to Route 53 \(step 12 of 14\)**  
We're confirming that the transfer process was successful\.

**Finalizing transfer \(step 13 of 14\)**  
We're setting up your domain in Route 53\.

**Transfer Complete \(step 14 of 14\)**  
Your transfer has been successfully completed\.