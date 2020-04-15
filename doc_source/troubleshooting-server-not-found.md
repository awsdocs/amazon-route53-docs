# My browser displays a "Server not found" error<a name="troubleshooting-server-not-found"></a>

If your browser displays a "Server not found" error when you try to browse to a domain \(example\.com\) or a subdomain \(www\.example\.com\), here are some common explanations\.

**Topics**
+ [You didn't create a record for the domain or subdomain name](#troubleshooting-server-not-found-no-resource-record-set)
+ [You created a record but specified the wrong value](#troubleshooting-server-not-found-wrong-value-in-resource-record-set)
+ [The resource that you're routing traffic to is unavailable](#troubleshooting-server-not-found-resource-unavailable)

## You didn't create a record for the domain or subdomain name<a name="troubleshooting-server-not-found-no-resource-record-set"></a>

If you don't create a record for the domain or subdomain, then DNS doesn't know where to route traffic when someone enters that name in a browser\. For more information, see [Working with records](rrsets-working-with.md)\.

## You created a record but specified the wrong value<a name="troubleshooting-server-not-found-wrong-value-in-resource-record-set"></a>

When you create a record, it's easy to specify the wrong value, such as the IP address for a web server or the domain name that CloudFront assigned to your web distribution\. If the record exists but you're still getting a "Server not found" error, we recommend that you confirm that the value is correct\. 

## The resource that you're routing traffic to is unavailable<a name="troubleshooting-server-not-found-resource-unavailable"></a>

If a record specifies a resource such as a web server that's unavailable, a browser will return a "Server not found" error\. We recommend that you check the status of the resource that you're routing traffic to\.