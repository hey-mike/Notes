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
