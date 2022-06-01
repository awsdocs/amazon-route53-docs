# Moving a geolocation to IP\-based routing<a name="resource-record-sets-move-geolocation-to-cidr"></a>

If you are using either geolocation or geoproximity routing policies, and you’re consistently seeing specific clients routed to an endpoint that isn’t optimal based on their physical location or network topology, you can better target these clients’ public IP ranges by using IP\-based routing\.

The following table contains an example geolocation configuration for an existing geolocation routing that we will fine\-tune for California IP ranges\.


| Record set name | Routing policy and origin | IP address of the application endpoint  | 
| --- | --- | --- | 
|  example\.com  |  Geolocation\-routing \(US\)  |  `198.51.100.1`  | 
|  example\.com  |  Geolocation\-routing \(EU\)   |  `198.51.100.2`  | 

To override IP ranges from California to go to a new application endpoint, first recreate the geolocation routing under a new record set name\.


| Record set name | Routing policy and origin | IP address of the application endpoint  | 
| --- | --- | --- | 
|  geo\.example\.com  |  Geolocation\-routing \(US\)  |  `198.51.100.1`  | 
|  geo\.example\.com  |  Geoloaction\-routing \(EU\)   |  `198.51.100.2`  | 

Then, create IP\-based routing records and a default record that points to your recently recreated geolocation routing recordset\. 


| Record set name | Routing policy and origin | IP address of the application endpoint  | 
| --- | --- | --- | 
|  example\.com  |  IP\-based routing \(default\)   |  Alias record to geo\.example\.com application endpoint that you want to be the default\. For example, `198.51.100.1`\.  | 
|  example\.com  |  IP\-based routing \(California IP ranges\)   |  `198.51.100.3`  | 