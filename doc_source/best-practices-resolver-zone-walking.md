# DNS zone walking<a name="best-practices-resolver-zone-walking"></a>

A DNS zone walking attack attempts to get all content from DNSSEC\-signed DNS zones\. If Route 53 Resolver team detects a traffic pattern that matches the ones generated when DNS zones are walked on your endpoint, the service team will throttle the traffic on your endpoint\. As a consequence you might observe a high percentage of your DNS queries timing out\.

If you observe reduced capacity on your endpoints and believe that the endpoint have been throttled erroneously, go to https://console\.aws\.amazon\.com/support/home\#/ to create a support case\. 