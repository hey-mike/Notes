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

- **tcp_keepalive_time** controls the time, in seconds, after which a keepalive packet is sent when no data has been sent by the socket (ACKs are not considered data). Amazon recommends
- **tcp_keepalive_intvl** controls the time, in seconds, between sending subsequent keepalive packets after the initial packet is sent (set using the tcp_keepalive_time parameter). Amazon recommends
- **tcp_keepalive_probes**is the number of unacknowledged keepalive probes that occur before the application is notified. Amazon recommends
