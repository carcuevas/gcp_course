# Google Cloud Storage

## Buckets
* Name should be unique across the Cloud Storage

* We need to take into consideration that to list the buckets inside of a project (Called *Class A Operations*) it's charged by 10.000 operations, if for example we want to list the object of a bucket (called *Class B Operations*) it is also charged by 10.000 operations and depending of the Storage Class 

### Storage Location for Buckets
We can have:
* **Multi-regional**: High availability - 99.95% of Availability SLA 
* **Dual-Region**: (Low latency but with High availability in 2 regions, more expensive one - 99.95%  of Availability SLA 
* **Regional**: Lowest latency but just in one region 99.90% of Availability SLA 


### Storage Class for Buckets
* **Standard**: The most expensive, but for frequently used data
* **Nearline**: For backups, when retrieving data once a month, cheaper. So the minimum time of archiving without paying penalty is 30 days.
* **Coldline**: Best for disaster recovery, or for retrieving data once a trimester. A bit cheaper than Nearline by GB stored. But the minimum time of archiving without paying penalty is 90 days.
* **Archive**: Long time digital preservation, accessed less than once a year. The cheapest one by GB, but take care with the *Class A* and *Class B* operations are quite expensive. The minimum time of archiving without paying penalty is 365 days
