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

- **Cluster**: A logical grouping of one or more nodes. If there is more than one node, there is a primary node and read replicas. A cluster can support up to ten nodes, and Amazon recommends a minimum of three nodes in a cluster with each node placed in a different Availability Zone.
