# Choosing Performant Databases

## AURORA

Amazon Aurora is a MySQL- and PostgreSQL-compatible relational database built by Amazon specifically for AWS

### When to Use T2 Instances

- Aurora MySQL instances that use the db.t2.small or db.t2.medium DB instance classes are best suited for applications that do not support a high workload for an extended amount of time.
- Using the db.t2.small and db.t2.medium DB instance classes only for development and test servers or other nonproduction servers.
- The MySQL Performance Schema should not be enabled on Aurora MySQL T2 instances. If the Performance Schema is enabled, the T2 instance might run out of memory.

### Recommendation the following when you use a T2 instance for the primary instance or Aurora Replicas in an Aurora MySQL DB cluster

- If you use a T2 instance as a DB instance class in your DB cluster, use the same DB instance class for all instances in the DB cluster.

- Monitor your CPU Credit Balance (CPUCreditBalance) to ensure that it is at a sustainable level.

- When you have exhausted the CPU credits for an instance, you see an immediate drop in the available CPU and an increase in the read and write latency for the instance; this results in a severe decrease in the overall performance of the instance. If your CPU credit balance is not at a sustainable level, modify your DB instance to use one of the supported R3 DB instance classes (scale compute).

- Monitor the replica lag (AuroraReplicaLag) between the primary instance and the Aurora Replicas in the Aurora MySQL DB cluster.

- If an Aurora Replica runs out of CPU credits before the primary instance, the lag behind the primary instance results in the Aurora Replica frequently restarting. If you see a sustained increase in replica lag, make sure that your CPU credit balance for the Aurora Replicas in your DB cluster is not being exhausted.

- Keep the number of inserts per transaction below 1 million for DB clusters that have binary logging enabled.

- If the DB cluster parameter group for your DB cluster has the binlog_format parameter set to a value other than OFF, your DB cluster might experience out-of-memory conditions if the DB cluster receives transactions that contain over 1 million rows to insert. Monitor the freeable memory (FreeableMemory) metric to determine whether your DB cluster is running out of available memory.

- Check the write operations (VolumeWriteIOPS) metric to see if your primary instance is receiving a heavy load of writer operations. If this is the case, update your application to limit the number of inserts in a transaction to fewer than 1 million; alternatively, you can modify your instance to use one of the supported R3 DB instance classes (scale compute)

### Work with Asynchronous Key Prefetch

Aurora can use **Asynchronous Key Prefetch** (AKP) to improve the performance of queries that join tables across indexes. This feature improves performance by anticipating the rows needed to run queries in which a JOIN query requires use of the **Batched Key Access** (BKA) Join algorithm and **Multi-Range Read** (MRR) optimization features.

### Avoid Multithreaded Replication

Aurora uses single-threaded replication when an Aurora MySQL DB cluster is used as a replication slave. While Aurora does not prohibit multithreaded replication, Aurora MySQL has inherited several issues regarding multithreaded replication from MySQL. Amazon recommends against the use of multithreaded replication in production.

### Use Scale Reads

You can use Aurora with your MySQL DB instance to take advantage of the read scaling capabilities of Aurora and expand the read workload for your MySQL DB instance. To use Aurora **to read scale your MySQL DB instance, create an Amazon Aurora MySQL DB cluster and make it a replication slave of your MySQL DB instance**. This applies to an Amazon RDS MySQL DB instance or a MySQL database running external to Amazon RDS.

### Consider Hash Joins

When you need to join a large amount of data by using an equijoin, a hash join can improve query performance

### Use TCP Keepalive Parameters

- **tcp_keepalive_time** controls the time, in seconds, after which a keepalive packet is sent when no data has been sent by the socket (ACKs are not considered data).
- **tcp_keepalive_intvl** controls the time, in seconds, between sending subsequent keepalive packets after the initial packet is sent (set using the tcp_keepalive_time parameter).
- **tcp_keepalive_probes** is the number of unacknowledged keepalive probes that occur before the application is notified.

## RDS

- Carefully monitor memory, CPU, and storage use with CloudWatch.

- Monitor performance metrics on a regular basis to see the average, maximum, and minimum values for a variety of time ranges.

- To be able to troubleshoot performance issues, understand the baseline performance of the system.

- Use CloudWatch events and alarms.

- Scale your DB instance as you approach capacity limits.

- Set a backup window to occur during times of traditionally low write IOPS.

- To increase the I/O capacity for a DB instance, migrate to a DB instance class with a higher I/O capacity. You can also upgrade from standard storage options, or you can provision additional throughput capacity.

- If your client application is caching the Domain Name Service (DNS) data of your DB instances, set a time-to-live (TTL) value of less than 30 seconds.

- Allocate enough RAM so that your working set resides almost completely in memory. Check the ReadIOPS metric while the DB instance is under load. The value of ReadIOPS should be small and stable.

- Because RDS provides metrics in real time for the operating system (OS) that your DB instance runs on, view the metrics for your DB instance using the console or consume the enhanced monitoring JSON output from CloudWatch logs in a monitoring system of your choice. Enhanced monitoring is available for all DB instance classes except for db.m1.small; enhanced monitoring is available in all regions except for AWS GovCloud (US).

- Tune your most commonly used and most resource-intensive queries to make them less expensive to run; this is one of the best ways to improve DB instance performance.

- Try out DB parameter group changes on a test DB instance as Amazon recommends before applying parameter group changes to your production DB instances.

## DYNAMODB

- In RDBMS, you design for flexibility without worrying about implementation details or performance. Query optimization generally does not affect schema design, but normalization is important.
- In DynamoDB, you design your schema specifically to make the most common and important queries as fast and as inexpensive as possible. Your data structures are tailored to the specific requirements of your business use cases.

### Before you begin

- **Data size**: Knowing how much data will be stored and requested at one time will help determine the most effective way to partition the data.

- **Data shape:** Instead of reshaping data when a query is processed (as an RDBMS system does), a NoSQL database organizes data so that its shape in the database corresponds with what will be queried. This is a key factor in increasing speed and scalability.

- **Data velocity:** DynamoDB scales by increasing the number of physical partitions that are available to process queries and by efficiently distributing data across those partitions. Knowing in advance what the peak query loads might be helps determine how to partition data to best use I/O capacity.

### Govern performance

- **Keep related data together**: Research on routing-table optimization in the late 1990s found that **“locality of reference”** was the single most important factor in speeding up response time: keeping related data together in one place. This is equally true in NoSQL systems today, where keeping related data in close proximity has a major impact on cost and performance. Instead of distributing related data items across multiple tables, you should keep related items in your NoSQL system as close together as possible.

- **As a general rule, maintain as few tables as possible in a DynamoDB application**: Most well-designed applications require only one table, unless you have a specific reason for using multiple tables. Exceptions are cases where high-volume time series data are involved, or data sets that have very different access patterns, but these are exceptions. A single table with inverted indexes can usually enable simple queries to create and retrieve the complex hierarchical data structures that your application requires.

- **Use sort order**: Related items can be grouped together and queried efficiently if their key design causes them to sort together. This is an important NoSQL design strategy.

- **Distribute queries**: It is also important that a high volume of queries not be focused on one part of the database, where they can exceed I/O capacity. Instead, you should design data keys to distribute traffic evenly across partitions as much as possible, avoiding hotspots.

- **Use global secondary indexes**: By creating specific global secondary indexes, you can enable different queries from those your main table can support, and that are still fast and relatively inexpensive.

### Model data

- The primary key that uniquely identifies each item in a DynamoDB table can be simple (a partition key only) or composite (a partition key combined with a sort key).

- Generally speaking, you should design your application for uniform activity across all logical partition keys in the table and its secondary indexes. You can determine the access patterns that your application requires and estimate the total Read Capacity Units (RCUs) and Write Capacity Units (WCUs) that each table and secondary index requires.

- As traffic starts to flow, DynamoDB automatically supports your access patterns using the throughput you have provisioned, as long as the traffic against a given partition key does not exceed 3000 RCUs or 1000 WCUs.

### Burst Capacity

- Whenever you are not fully using a partition’s throughput, DynamoDB reserves a portion of that unused capacity for later bursts of throughput to handle usage spikes.
- DynamoDB currently retains up to 5 minutes (300 seconds) of unused read and write capacity.
- DynamoDB can also consume burst capacity for background maintenance and other tasks without prior notice.

### Adaptive Capacity

- It is not always possible to distribute read and write activity evenly all the time.
- Adaptive capacity works by automatically increasing throughput capacity for partitions that receive more traffic
- Adaptive capacity is enabled automatically for every DynamoDB table, so you do not need to explicitly enable or disable it.
- Typically, a 5- to 30-minute interval occurs between the time that throttling of a hot partition begins and the time that adaptive capacity activates.

Well-designed **sort keys** have two key benefits:

- They gather related information together in one place where it can be queried efficiently. Careful design of the sort key lets you retrieve commonly needed groups of related items using range queries with operators such as starts-with, between, >, and <.
- Composite sort keys let you define hierarchical (one-to-many) relationships in your data that you can query at any level of the hierarchy

### Secondary Indexes

- **Global secondary index:** An index with a partition key and a sort key that can be different from those on the base table.
- **Local secondary index**: An index that has the same partition key as the base table but a different sort key.
- DynamoDB is limited to a maximum of five global secondary indexes and five local secondary indexes
- For global secondary indexes, this is less restrictive than it might appear because you can satisfy multiple application access patterns with one global secondary index by overloading it
- use global secondary indexes rather than local secondary indexes
- **when you need strong consistency in your query results** a local secondary index can provide but a global secondary index cannot (global secondary index queries only support eventual consistency).
- Keep the number of indexes to a minimum, indexes that are seldom used contribute to increased storage and I/O costs without improving application performance.
- A local secondary index can provide but a global secondary index cannot (global secondary index queries only support eventual consistency).
- Avoid indexing tables that experience heavy write activity.
- Because secondary indexes consume storage and provisioned throughput, you should keep the size of the index as small as possible. The smaller the index, the greater the performance advantage compared to querying the full table

### If you expect a lot of write activity on a table compared to reads, follow these best practices:

- Consider projecting fewer attributes to minimize the size of items written to the index. However, this advice applies only if the size of projected attributes would otherwise be larger than a single write capacity unit (1 KB). For example, if the size of an index entry is only 200 bytes, DynamoDB rounds this up to 1 KB. In other words, as long as the index items are small, you can project more attributes at no extra cost.

- Avoid projecting attributes that you know will rarely be needed in queries. Every time you update an attribute that is projected in an index, you incur the extra cost of updating the index as well. You can still retrieve nonprojected attributes in a query at a higher provisioned throughput cost, but the query cost may be significantly lower than the cost of updating the index frequently.

- Specify ALL only if you want your queries to return the entire table item sorted by a different sort key. Projecting all attributes eliminates the need for table fetches, but in most cases, it doubles your costs for storage and write activity.

- To get the fastest queries with the lowest possible latency, project all the attributes that you expect those queries to return. In particular, if you query a local secondary index for attributes that are not projected, DynamoDB automatically fetches those attributes from the table, which requires reading the entire item from the table. This introduces latency and additional I/O operations that you can avoid.

- When you create a local secondary index, think about how much data will be written to it and how many of those data items will have the same partition key value. If you expect that the sum of table and index items for a particular partition key value might exceed 10 GB, consider whether you should avoid creating the index.

- If you cannot avoid creating the local secondary index, anticipate the item collection size limit and take action before you exceed it.

### Querying and Scanning Data

- scan operations are less efficient than other operations in DynamoDB
- For faster response times, design your tables and indexes so that your applications can use query instead of scan.
- Alternatively, design your application to use scan operations in a way that minimizes the impact on your request rate.
- When you create a table, you set its read and write capacity unit requirements
- Because a scan operation reads an entire page (by default, 1 MB), you can reduce the impact of the scan operation by setting a smaller page size
- Many applications can benefit from using parallel scan operations rather than sequential scans.A parallel scan can be the right choice if the following conditions are met:
  - The table size is 20 GB or larger.
  - The table’s provisioned read throughput is not being fully used.
  - Sequential scan operations are too slow.

## ELASTICACHE

### Lazy Loading Versus Write Through

- Scenario 1: Cache Hit

  - When data is in the cache and isn’t expired:
  - Application requests data from the cache.
  - Cache returns the data to the application.

- Scenario 2: Cache Miss

  - When data isn’t in the cache or is expired:
  - Application requests data from the cache.
  - Cache doesn’t have the requested data, so it returns a null.
  - Application requests and receives the data from the database.
  - Application updates the cache with the new data.

### Advantages and Disadvantages of Lazy Loading

| Advantages                                                                                                      | Disadvantages                                                                                                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Only requested data is cached.                                                                                  | There is a cache miss penalty. Each cache miss results in three trips: the initial request for data from the cache; the query of the database for the data; and the writing of data to the cache, which can cause a noticeable delay in data getting to the application. |
| Because most data is never requested, lazy loading avoids filling up the cache with data that is not requested. | If data is written to the cache only when there is a cache miss, data in the cache can become stale because there are no updates to the cache when data is changed in the database. This issue is addressed by the write through and adding TTL strategies.              |
| Node failures are not fatal.                                                                                    |                                                                                                                                                                                                                                                                          |

### Advantages and Disadvantages of Write Through

| Advantages                                                                                                                                                                                                                                                                                                                                | Disadvantages                                                                                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Data in the cache is never stale: Because the data in the cache is updated every time it is written to the database, the data in the cache is always current.                                                                                                                                                                             | Missing data: In the case of spinning up a new node, whether due to a node failure or scaling out, there is missing data that continues to be missing until it is added or updated on the database. This situation can be minimized by implementing lazy loading in conjunction with write through. |
| Write penalty vs. read penalty: Every write involves two trips: a write to the cache and a write to the database. This adds latency to the process. That said, end users are generally more tolerant of latency when updating data than when retrieving data. There is an inherent sense that updates are more work and thus take longer. | Cache churn: Because most data is never read, a lot of data in the cluster is never read. This is a waste of resources. By adding TTL, you can minimize wasted space.                                                                                                                               |

### What Is TTL

Time to live (TTL) is an integer value that specifies the number of seconds (or milliseconds) until the key expires. When an application attempts to read an expired key, it is treated as though the key is not found, meaning that the database is queried for the key and the cache is updated. This does not guarantee that a value is not stale, but it keeps data from getting too stale and requires that values in the cache are occasionally refreshed from the database.

### Avoid Running Out of Memory When Executing a Background Write

- set reserved-memory-percent to 50 (50 percent) for Redis versions before 2.8.22 or 25 (25 percent) for Redis versions 2.8.22 and later.
- The default value for reserved-memory is 0, which allows Redis to consume all of maxmemory with data, potentially leaving too little memory for other uses, such as a background write process.

### How Much Reserved Memory Do You Need

If you are running a version of Redis prior to 2.8.22, you need to reserve more memory for backups and failovers than if you are running Redis 2.8.22 or later. This requirement is due to the different ways that ElastiCache for Redis implements the backup process. The guiding principle is to reserve half of a node type’s maxmemory value for Redis overhead for versions prior to 2.8.22 and one-fourth for Redis versions 2.8.22 and later.

### Parameters to Manage Reserved Memory

- reserved-memory and reserved-memory-percent
- Neither one of these parameters is part of the Redis distribution

### Online Cluster Resizing

- Recommendations on initiating resharding:

  - Test your application
  - Get early notification for scaling issues
  - Ensure sufficient free memory is available before scaling in
  - Initiate resharding during off-peak hours
  - Review client timeout behavior

- Recommendations on resharding

  - Avoid expensive commands
  - Follow Lua best practices

- After resharding
  - Scale-in might be partially successful if insufficient memory is available on target shards. If such a result occurs, review available memory and retry the operation, if necessary.
  - Slots with large items are not migrated. In particular, slots with items larger than 256 MB postserialization are not migrated.
  - The BRPOPLPUSH command is not supported if it operates on the slot being migrated. FLUSHALL and FLUSHDB commands are not supported inside Lua scripts during a resharding operation.

## REDSHIFT

> Amazon Redshift Spectrum allows you to store data in Amazon S3, in open file formats, and have it available for analytics without the need to load it into your Amazon Redshift cluster. It enables you to easily join data sets across Redshift clusters and S3 to provide unique insights that you would not be able to obtain by querying independent data silos.

### best practices

- Use a COPY command to load data.

- Use a single COPY command to load from multiple files.

- Split your load data into multiple files.

- Compress your data files.

- Use a manifest file.

- Verify data files before and after a load.

- Use a multi-row insert.

- Use a bulk insert.

- Load data in sort key order.

- Load data in sequential blocks.

- Use time-series tables.

- Use a staging table to perform a merge (Upsert).

- Schedule around maintenance windows.

### Best Practices for Designing Queries

- Design tables according to best practices to provide a solid foundation for query performance.

- Avoid using select \*. Include only the columns you specifically need.

- Use a CASE expression to perform complex aggregations instead of selecting from the same table multiple times.

- Don’t use cross-joins unless absolutely necessary. These joins without a join condition result in the Cartesian product of two tables. Cross-joins are typically executed as nested-loop joins, which are the slowest of the possible join types.

- Use subqueries in cases where one table in the query is used only for predicate conditions and the subquery returns a small number of rows (less than about 200).

- Use predicates to restrict the data set as much as possible. In the predicate, use the least expensive operators that you can. Comparison Condition operators are preferable to LIKE operators. LIKE operators are still preferable to SIMILAR TO or POSIX operators.

- Avoid using functions in query predicates. Using them can drive up the cost of the query by requiring large numbers of rows to resolve the intermediate steps of the query.

- If possible, use a WHERE clause to restrict the data set. The query planner can then use row order to help determine which records match the criteria, so it can skip scanning large numbers of disk blocks. Without this, the query execution engine must scan participating columns entirely.

- Add predicates to filter tables that participate in joins, even if the predicates apply the same filters. The query returns the same result set, but Amazon Redshift is able to filter the join tables before the scan step and can then efficiently skip scanning blocks from those tables. Redundant filters aren’t needed if you filter on a column that’s used in the join condition.

- Use sort keys in the GROUP BY clause so the query planner can use more efficient aggregation. A query might qualify for one-phase aggregation when its GROUP BY list contains only sort key columns, one of which is also the distribution key. The sort key columns in the GROUP BY list must include the first sort key, then other sort keys that you want to use in sort key order. For example, it is valid to use the first sort key; the first and second sort keys; the first, second, and third sort keys; and so on. It is not valid to use the first and third sort keys

### Work with Recommendations from Amazon Redshift Advisor

Advisor recommendations are made up of the following sections:

- Best practice recommendation: This is a brief summary of the recommendation.
- Observation: Findings from tests run on your cluster to determine if a test value is within a specified range.
- Recommendations: These recommendations provide specific steps to take and implementation tips
- Provide feedback: Your feedback can be detailed and goes directly to the Amazon Redshift engineering team.
