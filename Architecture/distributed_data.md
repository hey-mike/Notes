# Distributed Data

## reasons

- **Scalability**:If your data volume, read load, or write load grows bigger than a single machine can handle, you can potentially spread the load across multiple machines.

- **Fault tolerance/high availability**:If your application needs to continue working even if one machine (or several machines, or the network, or an entire datacenter) goes down, you can use multiple machines to give you redundancy. When one fails, another one can take over.

- **Latency**: If you have users around the world, you might want to have servers at various locations worldwide so that each user can be served from a datacenter that is geographically close to them. That avoids the users having to wait for network packets to travel halfway around the world.

## Replication

Replication means keeping a copy of the same data on multiple machines that are connected via a network.
There are several reasons why you might want to replicate data:

- To keep data geographically close to your users (and thus reduce access latency)

- To allow the system to continue working even if some of its parts have failed (and thus increase availability)

- To scale out the number of machines that can serve read queries (and thus increase read throughput)

## partitioning (sharding)

If the data that you’re replicating does not change over time, then replication is easy: you just need to copy the data to every node once, and you’re done. All of the difficulty in replication lies in handling changes to replicated data, and that’s what this chapter is about.

## Leaders and Followers

leader-based replication (also known as active/passive or master–slave replication):

1. One of the replicas is designated the **leader (also known as master or primary)**. When clients want to write to the database, they must send their requests to the leader, which first writes the new data to its local storage.

2. The other replicas are known as **followers (read replicas, slaves, secondaries, or hot standbys)**. Whenever the leader writes new data to its local storage, it also sends the data change to all of its followers as part of a replication log or change stream. Each follower takes the log from the leader and updates its local copy of the database accordingly, by applying all writes in the same order as they were processed on the leader.

3. When a client wants to read from the database, it can query either the leader or any of the followers. However, **writes are only accepted on the leader (the followers are read-only from the client’s point of view)**.

### Synchronous Versus Asynchronous Replication

1. Determining that the leader has failed
2. Choosing a new leader
3. Reconfiguring the system to use the new leader

## Multi-Leader Replication

1. Performance
   In a single-leader configuration, every write must go over the internet to the datacenter with the leader. This can add significant latency to writes and might contravene the purpose of having multiple datacenters in the first place. In a multi-leader configuration, every write can be processed in the local datacenter and is replicated asynchronously to the other datacenters. Thus, the inter-datacenter network delay is hidden from users, which means the perceived performance may be better.

2. Tolerance of datacenter outages
   In a single-leader configuration, if the datacenter with the leader fails, failover can promote a follower in another datacenter to be leader. In a multi-leader configuration, each datacenter can continue operating independently of the others, and replication catches up when the failed datacenter comes back online.

3. Tolerance of network problems
   Traffic between datacenters usually goes over the public internet, which may be less reliable than the local network within a datacenter. A single-leader configuration is very sensitive to problems in this inter-datacenter link, because writes are made synchronously over this link. A multi-leader configuration with asynchronous replication can usually tolerate network problems better: a temporary network interruption does not prevent writes being processed.
