# Choosing Performant Storage

## Performant S3 Services

- S3 automatically scales to high request rates. For example, your application can achieve at least 3,500 PUT/POST/DELETE and 5,500 GET requests per second per prefix in a bucket. There are no limits to the number of prefixes in a bucket. It is simple to increase your read or write performance exponentially. For example, if you create 10 prefixes in an S3 bucket to parallelize reads, you could scale your read performance to 55,000 read requests per second.

- If your S3 workload uses server-side encryption with AWS Key Management Service (KMS), you should reference the “AWS KMS Limits” section of the AWS Key Management Service Developer Guide for information about the request rates supported for your use case.

- **If your workload is mainly sending GET requests, you should consider using CloudFront in conjunction with S3 for performance optimization.** With CloudFront, you can distribute content to your users with low latency and a high data transfer rate. You also send fewer direct requests to S3. This can reduce storage costs.

- **TCP window scaling** allows you to improve network throughput performance between your operating system and application layer and S3 by supporting window sizes larger than 64 KB. At the start of the TCP session, a client advertises its supported receive window WSCALE factor, and S3 responds with its supported receive window WSCALE factor for the upstream direction.

- **TCP selective acknowledgment** is designed to improve recovery time after a large number of packet losses. TCP selective acknowledgment is supported by most newer operating systems but might have to be enabled.

### High workload environments

> Problem

- S3 maintains an index of object key names in each region.
- Object keys are stored in UTF-8 binary ordering across multiple partitions in the index.
- The key name determines which partition the key is stored in.
- Using a sequential prefix, such as a timestamp or a number sequence, increases the likelihood that S3 will target a specific partition for a large number of your keys. This can overwhelm the I/O capacity of the partition.

> Solution

- If your workload is a mix of request types, introduce some randomness to key names by adding a hash string as a prefix to the key name.
- When you introduce randomness to your key names, the I/O load is distributed across multiple index partitions.
- The following example shows key names with a four-character hexadecimal hash added as a prefix:
  - myexampleawsbucket/232a-2019-14-03-15-00-00/cust123/photo1.jpg
  - myexampleawsbucket/7b54-2019-14-03-15-00-00/cust123/photo2.jpg
  - myexampleawsbucket/921c-2019-14-03-15-00-00/cust345/photo3.jpg
  - myexampleawsbucket/ba65-2019-14-03-15-00-00/cust345/photo4.jpg
  - myexampleawsbucket/8761-2019-14-03-15-00-00/cust345/photo5.jpg

Without the four-character hash prefix, S3 might distribute all of this load to one or two index partitions because the name of each object begins the same and all objects in the index are stored in alphanumeric order. The four-character hash prefix ensures that the load is spread across multiple index partitions.

**If your workload is sending mainly GET requests,** you can add randomness to key names. You can also integrate CloudFront with S3 to distribute content to your users with low latency and a high data transfer rate.

> Note: Amazon has offered increased performance for S3 across all regions and has applied this to all S3 implementations with no intervention required from you. Amazon made this announcement: “This S3 request rate performance increase removes any previous guidance to randomize object prefixes to achieve faster performance. That means you can now use logical or sequential naming patterns in S3 object naming without any performance implications.” Amazon has indicated it will be modifying its certification exams to reflect this. We decided to keep the “legacy” information in this text regarding sequential naming patterns in case you still encounter such questions on your test date.

### CLI

- If the S3 buckets are in the same region, you can use the AWS CLI to simultaneously run multiple instances of the S3 **cp (copy)**, **mv (move)**, or **sync (synchronize)** commands with the --exclude filter to increase performance through multithreading.
- use the **-** option to stream to stdout and then pipe that into another command where the source is stdin.

```bash
aws s3 cp s3://bucketa/image.png - | aws s3 cp - s3://bucketb/image.png
```

> For large file: You should also consider using Snowball for these S3 uploads or downloads. Snowball is a petabyte-scale data transport solution that uses secure appliances to transfer large amounts of data into and out of AWS.

## Performant EBS Services

### Guidelines

- On instances without support for EBS-optimized throughput, network traffic can contend with traffic between your instance and your EBS volumes; on EBS-optimized instances, the two types of traffic are kept separate.

- When you measure the performance of your EBS volumes, it is important to understand the units of measure involved and how performance is calculated. For example, IOPS are a unit of measure representing input/output operations per second. The operations are measured in KB, and the underlying drive technology determines the maximum amount of data that a volume type counts as a single I/O. I/O size is capped at 256 KB for SSD volumes and 1,024 KB for HDD volumes because SSD volumes handle small or random I/O much more efficiently than HDD volumes. When small I/O operations are physically contiguous, EBS attempts to merge them into a single I/O up to the maximum size.

- There is a relationship between the maximum performance of your EBS volumes, the size and number of I/O operations, and the time it takes for each action to complete. Each of these factors affects the others, and different applications are more sensitive to one factor or another.

- There is a significant increase in latency when you first access each block of data on a new EBS volume that was restored from a snapshot. You can avoid this performance hit by accessing each block prior to putting the volume into production. This process is called initialization (pre-warming). Some tools that exist will perform reads of all the blocks for you in order to achieve this.

- When you create a snapshot of a Throughput Optimized HDD (st1) or Cold HDD (sc1) volume, performance may drop as far as the volume’s baseline value while the snapshot is in progress. This behavior is specific to these volume types.

- Other factors that can limit performance include driving more throughput than the instance can support, the performance penalty encountered while initializing volumes restored from a snapshot, and excessive amounts of small, random I/O on the volume.

- **Your performance can also be affected if your application is not sending enough I/O requests**. You can monitor this by looking at your volume’s queue length and I/O size. The queue length is the number of pending I/O requests from your application to your volume. For maximum consistency, HDD-backed volumes must maintain a queue length (rounded to the nearest whole number) of 4 or more when performing 1 MB sequential I/O.

- Some workloads are read-heavy and access the block device through the operating system page cache (for example, from a file system). In this case, if you want to achieve the maximum throughput, Amazon recommends that you configure the read-ahead setting to 1 MB. This is a per-block-device setting that should be applied only to your HDD volumes.

- Some instance types can drive more I/O throughput than what you can provide for a single EBS volume. You can join multiple gp2, io1, st1, or sc1 volumes together in a RAID 0 configuration to use the available bandwidth for these instances.

- When you plan and configure EBS volumes for your application, it is important to consider the configuration of the instances that you will attach the volumes to. To get the most performance from your EBS volumes, you should attach them to an instance with enough bandwidth to support your volumes, such as an EBS-optimized instance or an instance with 10 Gigabit network connectivity. This is especially important when you stripe multiple volumes together in a RAID configuration.

- Launching an instance that is EBS-optimized provides you with a dedicated connection between your EC2 instance and your EBS volume. However, it is still possible to provision EBS volumes that exceed the available bandwidth for certain instance types, especially when multiple volumes are striped in a RAID configuration. Be sure to choose an EBS-optimized instance that provides more dedicated EBS throughput than your application needs; otherwise, the EBS to EC2 connection becomes a performance bottleneck.

- On a given volume configuration, certain I/O characteristics drive the performance behavior for your EBS volumes. SSD-backed volumes—General Purpose SSD (gp2) and Provisioned IOPS SSD (io1)—deliver consistent performance whether an I/O operation is random or sequential. HDD-backed volumes—Throughput Optimized HDD (st1) and Cold HDD (sc1)—deliver optimal performance only when I/O operations are large and sequential.

- The **volume queue length** is the number of pending I/O requests for a device. **Latency** is the true end-to-end client time of an I/O operation—in other words, the time elapsed between sending an I/O to EBS and receiving an acknowledgment from EBS that the I/O read or write is complete. Queue length must be correctly calibrated with I/O size and latency to avoid creating bottlenecks either on the guest operating system or on the network link to EBS. Optimal queue length varies for each workload, depending on your particular application’s sensitivity to IOPS and latency.

- For SSD-backed volumes, if your I/O size is very large, you may experience a smaller number of IOPS than you provisioned because you are hitting the throughput limit of the volume.

## Performant EFS services

|                             |              EFS              | EBS Provisioned IOPS         |
| --------------------------- | :---------------------------: | ---------------------------- |
| Per-operation latency       |    Low, consistent latency    | Lowest consistent latency    |
| Throughput scale            |       10+ GB per second       | Up to 2 GB per second        |
| Availability and durability | Redundant across multiple AZs | Redundant within a single AZ |
| Access                      |           Thousands           | Single instance              |

### Performance modes

- **General Purpose** is ideal for latency-sensitive use cases, like web-serving environments, content management systems, home directories, and general file serving. If you do not choose a performance mode when you create your file system, EFS selects the General Purpose mode for you by default.

- **Max I/O mode** can scale to higher levels of aggregate throughput and operations per second with a trade-off of slightly higher latencies for file operations. Highly parallelized applications and workloads, such as big data analysis, media processing, and genomics analysis, can benefit from this mode.

### Throughput modes

- With Bursting Throughput mode, throughput on EFS scales as your file system grows.
- With Provisioned Throughput mode, you can instantly provision the throughput of your file system (in MB/s) independent of the amount of data stored.

### Credit system

- EFS uses a credit system to determine when file systems can burst. Each file system earns credits over time at a baseline rate that is determined by the size of the file system and uses credits whenever it reads or writes data.
- Accumulated burst credits give the file system the ability to drive throughput above its baseline rate.
- When a file system has a positive burst credit balance, it can burst.

### When using EFS, keep the following performance tips in mind:

- **Average I/O Size**: The distributed nature of EFS enables high levels of availability, durability, and scalability. This distributed architecture results in a small latency overhead for each file operation. Due to this per-operation latency, overall throughput increases as the average I/O size increases because the overhead is amortized over a larger amount of data.

- **Simultaneous Connections**: EFS file systems can be mounted on up to thousands of EC2 instances concurrently. If you can parallelize your application across more instances, you can drive higher throughput levels on your file system in aggregate across instances.

- **Request Model**: By enabling asynchronous writes to your file system, pending write operations are buffered on the EC2 instance before they are written to EFS asynchronously. Asynchronous writes typically have lower latencies. When performing asynchronous writes, the kernel uses additional memory for caching. A file system that has enabled synchronous writes, or one that opens files using an option that bypasses the cache (for example, O_DIRECT), issues synchronous requests to EFS. Every operation goes through a round trip between the client and EFS.

- **NFS Client Mount Settings**: Verify that you are using the recommended mount options as outlined in Mounting File Systems and in Additional Mounting Considerations. EFS supports the Network File System versions 4.0 and 4.1 (NFSv4) and NFSv4.0 protocols when mounting your file systems on EC2 instances. NFSv4.1 provides better performance.

- **EC2 Instances:** Applications that perform a large number of read and write operations likely need more memory or computing capacity than applications that do not. When launching your EC2 instances, choose instance types that have the amount of these resources that your application needs. The performance characteristics of EFS file systems do not depend on the use of EBS-optimized instances.

- **Encryption:** EFS supports two forms of encryption: encryption in transit and encryption at rest. This option is for encryption at rest. Choosing to enable either or both types of encryption for your file system has a minimal effect on I/O latency and throughput.

## PERFORMANT GLACIER SERVICES

- When uploading large archives (100MB or larger), you can use multipart upload to achieve higher throughput and reliability. Multipart uploads allow you to break your large archive into smaller chunks that are uploaded individually. After all the constituent parts are successfully uploaded, they are combined into a single archive.

- Standard retrievals allow you to access any of your archives within several hours. Standard retrievals typically complete within 3–5 hours.

- Bulk retrievals are Glacier’s lowest-cost retrieval option, enabling you to retrieve large amounts, even petabytes, of data inexpensively in a day. Bulk retrievals typically complete within 5–12 hours.

- Expedited retrievals allow you to quickly access your data when occasional urgent requests for a subset of archives are required. For all but the largest archives (250 MB+), data accessed using expedited retrievals is typically made available within 1–5 minutes. There are two types of expedited retrievals: On-Demand and Provisioned.

- On-Demand requests are like EC2 On-Demand instances and are available the vast majority of the time.

- Provisioned Capacity guarantees that your retrieval capacity for expedited retrievals will be available when you need it. Each unit of capacity ensures that at least three expedited retrievals can be performed every 5 minutes and provides up to 150 MB/s of retrieval throughput.
