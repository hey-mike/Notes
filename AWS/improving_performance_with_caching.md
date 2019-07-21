# Improving Performance with Caching

## ELASTICACHE

- There is support for Redis and memcached.
- memcached is a simple service, whereas Redis provides support for more complex data types and storage approaches
- Redis also supports multi-AZ deployments inside AWS.

## DYNAMODB ACCELERATOR

DAX is a DynamoDB-compatible caching service that enables you to benefit from fast in-memory performance for demanding applications. DAX addresses **three core scenarios**:

- As an in-memory cache, DAX reduces the response times of eventually consistent read workloads by an order of magnitude from single-digit milliseconds to microseconds.

- DAX reduces operational and application complexity by providing a managed service that is API-compatible with Amazon DynamoDB and thus requires only minimal functional changes to use with an existing application.

- For read-heavy or bursty workloads, DAX provides increased throughput and potential operational cost savings by reducing the need to overprovision read capacity units. This capability is especially beneficial for applications that require repeated reads for individual keys.

**DAX is not always an ideal solution**. For example, DAX would not be appropriate under these conditions:

- For applications that require strongly consistent reads (or cannot tolerate eventually consistent reads)

- For applications that do not require microsecond response times for reads or that do not need to offload repeated read activity from underlying tables

- For applications that are write-intensive or that do not perform much read activity

- For applications that are already using a different caching solution with DynamoDB and are using their own client-side logic for working with that caching solution

DAX functions thanks to the following components:

- **Nodes**: The smallest building blocks of DAX. Each node contains a single replica of the cached data for DynamoDB. You can scale your DAX cluster by adding nodes to the cluster or by using larger node types or both.

- **Cluster**: A logical grouping of one or more nodes. If there is more than one node, there is a primary node and read replicas. A cluster can support up to ten nodes, and Amazon recommends **a minimum of three nodes in a cluster with each node placed in a different Availability Zone.**

## CLOUDFRONT

CloudFront speeds up distribution of your content to your end users. It does this by delivering content from a worldwide network of **data centers called** **edge locations**. As with all caching solutions, the content might not be available in the cache for an end user (cache miss). When this happens, CloudFront can retrieve the content from an origin that you have defined. This location might be an S3 bucket or a web server that you have identified as the source of your content.

## GREENGRASS

This service falls under the Internet of Things (IoT) category. It allows IoT devices to collect and analyze data closer to the source on-premises and communicate this information with each other securely on the on-premises network. A common example of Greengrass usage is the development of serverless code (Lambda functions) written in AWS and then seamlessly delivered to IoT devices for local execution.

Fortunately, the IoT devices do not need to maintain constant connectivity to the cloud for Greengrass to function. **Greengrass provides a local publisher/subscriber message manager** that can buffer messages to and from the cloud when connectivity is disrupted

## ROUTE 53

- **Alias record**: This is a type of record you can create with Amazon Route 53 to direct traffic to AWS resources you control, such as CloudFront distributions or Amazon S3 buckets.

  > Unlike a CNAME record, you can create an alias record at the top node of a DNS namespace, also known as the **zone apex**. For example, if you register the DNS name ajsnetworking.com, the zone apex is ajsnetworking.com. You cannot create a CNAME record for ajsnetworking.com, but you can create an alias record for the zone apex that routes traffic to www.ajsnetworking.com.

- **Authoritative name server:** This name server has definitive information about one part of the overall DNS system. A great example is an authoritative name server for the .com top-level domain (TLD). This name server knows the addresses of the name servers for every registered .com domain (that is a lot!); it returns this information when a user asks for it from a DNS resolver.

- **Authoritative name server**: This name server has definitive information about one part of the overall DNS system. A great example is an authoritative name server for the .com top-level domain (TLD). This name server knows the addresses of the name servers for every registered .com domain (that is a lot!); it returns this information when a user asks for it from a DNS resolver.

- **DNS resolver**: This DNS server acts as an intermediary between user requests (queries) and name servers; this is what you typically end up using when you send a DNS query from your web browser for a URL. Your system uses a DNS resolver managed by your ISP; it is often called a **recursive name server** because it sends requests to a sequence of authoritative name servers until it gets the response it needs.

- **Hosted zone**: This is a container object for the DNS records. It has the same name as the corresponding zone name; for example, my domain ajsnetworking.com has a hosted zone that **contains the records** for name resolution of my web server and mail server. It also **contains information about my subdomains** like private.ajsnetworking.com.

- **Private DNS**: This local version of Route 53 services directs traffic only for resources within your private VPCs in AWS.

- **DNS record**: This record enables you to determine how you want to direct traffic. For example, in my ajsnetworking.com domain, there is a DNS record for one of my web servers at 69.163.163.123.

- **Reusable delegation set**: You can use this set of four authoritative name servers with more than one hosted zone; this capability is useful when you are migrating a large number of zones to AWS.

- **Routing policy**: This setting for records controls query responses. Options are

  - **Simple routing policy**: This policy is used to direct traffic to a single resource that provides a given function—for example, a web server.

  - **Failover routing policy**: This policy can be used with active-passive failover.

  - **Geolocation routing policy**: This policy can be used to direct traffic to resources that are geographically close to users.

  - **Latency routing policy**: This policy is used to direct traffic to the lowest latency resource.

  - **Multivalue answer routing policy**: With this policy, DNS responds with up to eight healthy records selected at random.

  - **Weighted round robin**: This policy is used to direct traffic to multiple resources based on proportions that you can specify.

  - **Time to live (TTL)**: This policy sets the amount of time (in seconds) that you want a DNS resolver to cache the values for a record before submitting another request to Route 53 for current values of that record.

- When Route 53 returns a record with a TTL set to a fairly high value, your resolver will be able to service that client again quickly, as well as other clients looking for the same resource.
- Charges are based on, in part, the number of requests that Route 53 must respond to. you would need to set a small TTL if you are dealing with records that do, for whatever reason, change frequently.
- If you want rapid failover to occur, short TTLs are a must.
