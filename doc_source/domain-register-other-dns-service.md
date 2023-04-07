# Updating name servers to use another registrar<a name="domain-register-other-dns-service"></a>

If you want to move DNS management to another registrar, you need to update the name servers to point to 

**Note**  
We're updating the domains console for Route 53\. During the transition period, you can continue to use the old console\.

Choose the tab for the console that you are using\.
+ [New console](#register_other_dns_service_new_console)
+ [Old console](#register_other_dns_service_old_console)

------
#### [ New console ]<a name="domain-register-other-dns-service-new-procedure"></a>

**To update the name servers for your domain when you want to use another DNS service**

1. Use the process that is provided by your DNS service to get the name servers for the domain\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered domains**\.

1. Choose the name of the domain that you want to configure to use another DNS service\.

1. In the **Details** section, under the **Actions** drop\-down, choose **Edit name servers**\.

1. Delete the existing name servers, and then add the names of the name servers to the name servers that you got from your DNS service in step 1\.

1. Choose **Save changes**\.

1. \(Optional\) Delete the hosted zone that Route 53 created automatically when you registered your domain\. This prevents you from being charged for a hosted zone that you aren't using\.

   1. In the navigation pane, choose **Hosted Zones**\.

   1. Select the radio button for the hosted zone that has the same name as your domain\.

   1. Choose **Delete Hosted Zone**\.

   1. Choose **Confirm** to confirm that you want to delete the hosted zone\.

------
#### [ Old console ]<a name="domain-register-other-dns-service-procedure"></a>

**To update the name servers for your domain when you want to use another DNS service**

1. Use the process that is provided by your DNS service to get the name servers for the domain\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to configure to use another DNS service\.

1. Choose **Add/Edit Name Servers**\.

1. Change the names of the name servers to the name servers that you got from your DNS service in step 1\.

1. Choose **Update**\.

1. \(Optional\) Delete the hosted zone that Route 53 created automatically when you registered your domain\. This prevents you from being charged for a hosted zone that you aren't using\.

   1. In the navigation pane, choose **Hosted Zones**\.

   1. Select the radio button for the hosted zone that has the same name as your domain\.

   1. Choose **Delete Hosted Zone**\.

   1. Choose **Confirm** to confirm that you want to delete the hosted zone\.

------