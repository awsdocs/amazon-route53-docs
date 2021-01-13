# Location \(geolocation records\)<a name="record-geolocation-location"></a>

When you configure Route 53 to respond to DNS queries based on the location that the queries originated from, choose the continent, country, or United States state for which you want Route 53 to respond with the settings in this record\. 

**Note**  
We recommend that you create one geolocation record that has a value of **Default** for **Location**\. This record covers geographic locations that you haven't created records for and DNS queries that Route 53 can't identify a location for\.

## Learn more<a name="record-geolocation-location-learn-more"></a>
+ [Working with records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/rrsets-working-with.html)