# Cost-Optimized Storage

## S3 SERVICES

- There is no data transfer charge for data transferred within a Region. There is **only a charge for such a transfer when it is between Regions**.

- There is no data transfer charge for data transferred between EC2 and S3 in the same Region.

- There is no data transfer charge for data transferred between the EC2 Northern Virginia Region and S3 US East (Northern Virginia) Region. These are effectively the same Region; thus, there is no charge.

- S3 is part of the free tier. You can get started for free in all Regions except the AWS GovCloud Region. You receive **5 GB of S3 Standard for free**, including 20,000 GET Requests, 2000 PUT Requests, 15 GB of data transfer in, and 15 GB of data transfer out each month for one year.

### if you are outside the free tier

- **Storage Used**: This charge is based on average storage throughout the month.

- **Network Data Transferred In**: This charge represents the amount of data sent to your S3 buckets. Although this information is tracked in AWS, there is no charge for it.

- **Network Data Transferred Out**: This charge applies whenever data is read from any of your buckets outside the given S3 Region.

- **Data Requests:** These charges include PUT requests, GET requests, and DELETE requests.

- **Data Retrieval**: These charges apply to the S3 Standard-Infrequent Access and S3 One Zone-IA storage classes.

### Cost control

- Although versioning is excellent for fault tolerance and backup strategies, it can dramatically increase storage costs.
- You can control costs by automating the movement of objects in S3 to different storage tiers using Lifecycle Management.

## EBS SERVICES

- You pay for provisioned storage, not just used storage. Overprovisioning storage can add up across an infrastructure
- Remember that it is better to grow the EBS volume as time goes on and minimize white space (unless the white space is needed for IOPS requirements).
- You are still billed for EBS volumes even if they are disconnected from any EC2 instance. An excellent cost-saving strategy in this case is to take a snapshot of the volume and then delete it so that you no longer incur the charges for EBS.

### Examples of pricing in the US West (Oregon) Region

| Volume Type              | Price                                                               |
| ------------------------ | ------------------------------------------------------------------- |
| General-Purpose SSD      | \$0.10 per GB per month                                             |
| Provisioned IOPS SSD     | \$0.125 per GB per month and \$0.065 per provisioned IOPS per month |
| Throughput Optimized HDD | \$0.045 per GB per month                                            |
| Cold HDD                 | \$0.025 per GB per month                                            |
| Snapshots                | \$0.05 per GB per month                                             |

## EFS SERVICES

- There are additional charges for EFS File Sync. This is a pay-as-you-go model for data copied to EFS on a per-gigabyte basis. You can easily track this service with Amazon CloudWatch. The US West (Oregon) EFS File Sync price per month per gigabyte is \$0.01.

- In the default EFS Bursting Throughput mode, there is no charge for transfers as described previously given a baseline rate of 50 KB/s per gigabyte of throughput. The cost of EFS in US West (Oregon) given this default mode is \$0.30 per gigabyte per month.

- There is an optional EFS Provisioned Throughput mode. You are charged only above the baseline rate of 50 KB/s per gigabyte of throughput. The charge in US West (Oregon) is \$6.00 per MB/s per month.

- EFS can be perceived as being much more expensive than EBS. For example, EBS typically costs around $0.10/GB while EFS would be $0.30/GB. In reality, however, you save money due to no overprovisioning (you pay only for actual usage). Also, if you have a replicated HA/FT environment, you would need multiple EC2 instances with multiple attached EBS volumes. This will typically be far more expensive than using EFS. For example, consider a three–web server farm, with three Availability Zones (AZs; each with EBS volumes attached). Assuming full replication among all three instances, you would NET \$0.30/GB of stored data anyhow—the cost of EC2 processing, cross-AZ transfer fees, and additional overprovisioned storage in EBS. This makes EFS far cheaper.

## GLACIER SERVICES

- archives in Glacier have a minimum of 90 days of storage.
- there are no charges for data transfers under certain scenarios. For example, there are no data transfer charges when transferring between EC2 and Glacier in the same Region.

### Retrieve storage from Glacier

- **Expedited retrieval**: This cost is $0.03 per gigabyte and $0.01 per request.

- **Standard retrieval**: This cost is $0.01 per gigabyte and $0.05 per 1000 requests.

- **Bulk retrieval**: This cost is $0.0025 per gigabyte and $0.025 per 1000 requests.
