1. Weighted routing: Use this when you want to split traffic by percentage, like 80% to one endpoint and 20% to another. Route 53 uses the weight values as a ratio.

2. Latency routing: Use this when you have resources in multiple AWS Regions and want users sent to the region with the lowest latency. In CloudFormation, you specify the Region property on each record.

3. Geolocation routing: Use this when you want traffic routed based on where the DNS query comes from. In CloudFormation, this is done with the GeoLocation property. You can match continent, country, or subdivision, and AWS documents a default/fallback geolocation behavior for broader locations.

4. Failover routing: Use this for active-passive behavior: one primary endpoint and one secondary endpoint. Route 53 failover uses health checks or evaluated target health to decide when to switch.