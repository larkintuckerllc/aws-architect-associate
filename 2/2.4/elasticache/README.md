# Amazon ElastiCache

## Concepts

> Amazon ElastiCache is a web service that makes it easy to set up, manage, and scale a distributed in-memory data store or cache environment in the cloud. It provides a high-performance, scalable, and cost-effective caching solution. At the same time, it helps remove the complexity associated with deploying and managing a distributed cache environment.

## Overview

> A node is the smallest building block of an ElastiCache deployment. A node can exist in isolation from or in some relationship to other nodes.

&nbsp;

> Every node within a cluster is the same instance type and runs the same cache engine. Each cache node has its own Domain Name Service (DNS) name and port.

&nbsp;

> Cache parameter groups are an easy way to manage runtime settings for supported engine software. Parameters are used to control memory usage, eviction policies, item sizes, and more. An ElastiCache parameter group is a named collection of engine-specific parameters that you can apply to a cluster. By doing this, you make sure that all of the nodes in that cluster are configured in exactly the same way.

&nbsp;

> ElastiCache security groups are only applicable to clusters that are not running in an Amazon Virtual Private Cloud (Amazon VPC) environment. If you run your ElastiCache nodes in a virtual private cloud (VPC) based on Amazon VPC, you control access to your cache clusters with Amazon VPC security groups.

&nbsp;

> A subnet group is a collection of subnets (typically private) that you can designate for your clusters running in an Amazon VPC environment.

-AWS-[ElastiCache for Redis Components and Features](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.Components.html)

## Redis

> A Redis shard (called a node group in the API and CLI) is a grouping of one to six related nodes. A Redis (cluster mode disabled) cluster always has one shard. A Redis (cluster mode enabled) cluster can have 1–90 shards.

&nbsp;

> A multiple node shard implements replication by having one read/write primary node and 1–5 replica nodes.

&nbsp;

> A Redis cluster is a logical grouping of one or more ElastiCache for Redis Shards. Data is partitioned across the shards in a Redis (cluster mode enabled) cluster.

&nbsp;

> The endpoint for a single node Redis cluster is used to connect to the cluster for both reads and writes.

&nbsp;

> A multiple node Redis (cluster mode disabled) cluster has two types of endpoints. The primary endpoint always connects to the primary node in the cluster, even if the specific node in the primary role changes. Use the primary endpoint for all writes to the cluster.

&nbsp;

> The read endpoint in a Redis (cluster mode disabled) cluster always points to a specific node. Whenever you add or remove a read replica, you must update the associated node endpoint in your application.

&nbsp;

> A Redis (cluster mode enabled) cluster has a single configuration endpoint. By connecting to the configuration endpoint, your application is able to discover the primary and read endpoints for each shard in the cluster.

-AWS-[ElastiCache for Redis Components and Features](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/WhatIs.Components.html)

> You can now use a single reader endpoint to connect to your Redis read replicas. Until today, to easily connect to your read replicas you had to manage multiple endpoints at the application level. The new feature allows you to direct all read traffic to your ElastiCache for Redis cluster through a single, cluster-level endpoint.

-AWS-[Amazon ElastiCache launches reader endpoints for Redis](https://aws.amazon.com/about-aws/whats-new/2019/06/amazon-elasticache-launches-reader-endpoint-for-redis/)

> In-transit encryption encrypts your data whenever it is moving from one place to another, such as between nodes in your cluster or between your cluster and your application.

&nbsp;

> At-rest encryption encrypts your on-disk data during sync and backup operations.

&nbsp;

> Optionally, you can also use AUTH and the AUTH token (password) needed to perform operations on this cluster or replication group.

-AWS-[Data Security in Amazon ElastiCache](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/encryption.html)

To minimize the impact of a node failure, we recommend that your implementation use multiple nodes in each shard and distribute the nodes across multiple Availability Zones.

When running Redis, we recommend that you enable Multi-AZ on your replication group so that ElastiCache will automatically fail over to a replica if the primary node fails.

Amazon ElastiCache clusters running Redis can back up their data. You can use the backup to restore a cluster or seed a new cluster. The backup consists of the cluster's metadata, along with all of the data in the cluster. All backups are written to Amazon Simple Storage Service (Amazon S3), which provides durable storage. At any time, you can restore your data by creating a new Redis cluster and populating it with data from a backup. With ElastiCache, you can manage backups using the AWS Management Console, the AWS Command Line Interface (AWS CLI), and the ElastiCache API.

For production use, we strongly recommend that you always enable Redis backups,
and retain them for a minimum of 7 days. In practice, retaining them for 14 or 30 days
will provide better safety in the event of an application bug that ends up corrupting data.

**note:** AWS has a propetary automatic re-sharing approach that involves no downtime.

Redis has two categories of data structures: simple keys and counters, and
multidimensional sets, lists, and hashes. The bad news is the second category cannot
be sharded horizontally. But the good news is that simple keys and counters can.

## MemCache

> The Memcached engine supports Auto Discovery. Auto Discovery is the ability for client programs to automatically identify all of the nodes in a cache cluster, and to initiate and maintain connections to all of these nodes. With Auto Discovery, your application doesn't need to manually connect to individual nodes. Instead, your application connects to a configuration endpoint.

&nbsp;

> When you run the Memcached engine, clusters can be made up of 1–20 nodes. You partition your database across the nodes. Your application reads and writes to each node's endpoint.

-AWS-[ElastiCache for Memcached Components and Features](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/WhatIs.Components.html)

### Backup

> Amazon ElastiCache clusters running Redis can back up their data. You can use the backup to restore a cluster or seed a new cluster. The backup consists of the cluster's metadata, along with all of the data in the cluster. All backups are written to Amazon Simple Storage Service (Amazon S3), which provides durable storage. At any time, you can restore your data by creating a new Redis cluster and populating it with data from a backup.

&nbsp;

> Backup window – A period during each day when ElastiCache begins creating a backup. The minimum length for the backup window is 60 minutes

&nbsp;

> The maximum backup retention limit is 35 days. If the backup retention limit is set to 0, automatic backups are disabled for the cluster.

-AWS-[Scheduling Automatic Backups](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/backups-automatic.html)

### Caching Strategies

> Lazy Loading: Amazon ElastiCache is an in-memory key-value store that sits between your application and the data store (database) that it accesses. Whenever your application requests data, it first makes the request to the ElastiCache cache. If the data exists in the cache and is current, ElastiCache returns the data to your application. If the data doesn't exist in the cache or has expired, your application requests the data from your data store. Your data store then returns the data to your application. Your application next writes the data received from the store to the cache. This way, it can be more quickly retrieved the next time it's requested.

&nbsp;

> The disadvantages of lazy loading are as follows:

- There is a cache miss penalty.

- Stale data

Apply a lazy caching strategy anywhere in your application where you have data that is
going to be read often, but written infrequently.

> Write-Through: The write-through strategy adds data or updates data in the cache whenever data is written to the database.

&nbsp;

> The disadvantages of write-through are as follows:

- Missing data: If you spin up a new node, whether due to a node failure or scaling out, there is missing data. This data continues to be missing until it's added or updated on the database. You can minimize this by implementing lazy loading with write-through.

- Cache churn: Most data is never read, which is a waste of resources. By adding a time to live (TTL) value, you can minimize wasted space.

-AWS-[Caching Strategies](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Strategies.html)

### Monitoring

> The following CloudWatch metrics offer good insight into ElastiCache performance. In most cases, we recommend that you set CloudWatch alarms for these metrics so that you can take corrective action before performance issues occur.

- CPUUtilization: This is a host-level metric reported as a percentage. For more information, see Host-Level Metrics. Generally speaking, we suggest you set your threshold at 90% of your available CPU.

(Redis) Because Redis is single-threaded, the actual threshold value should be calculated as a fraction of the node's total capacity.

For Redis, ElastiCache provides two different types of metrics for monitoring CPU
usage: CPUUtilization and EngineCPUUtilization. Because Redis is single-threaded,
you need to multiply the CPU percentage by the number of cores to get an accurate
measure of CPUUtilization. For smaller node types with one or two vCPUs, use the
CPUUtilization metric to monitor your workload. For larger node types with four or more
vCPUs, we recommend monitoring the EngineCPUUtilization metric, which reports the
percentage of usage on the Redis engine core. 

- SwapUsage: This metric should not exceed 50 MB.

- Evictions: recommend that you determine your own alarm threshold

- CurrConnections: recommend that you determine your own alarm threshold

In extreme cases, a single hot cache key can create a hot spot that overwhelms a single
cache node. In this case, having good metrics about your cache, especially your most
popular cache keys, is crucial to designing a solution. One solution is to create a
mapping table that remaps very hot keys to a separate set of cache nodes. 

### More Caching Strategies - Memcached

Problem with Memcached and simple sharding approach:

Unfortunately, this particular approach suffers from a fatal flaw due to the way that
modulo works. As the number of cache nodes scales up, most hash keys will get
remapped to new nodes with empty caches, as a side effect of using modulo. You can
calculate the number of keys that would be remapped to a new cache node by dividing
the old node count by the new node count.

Luckily, many modern client libraries include consistent hashing. Although you shouldn't
need to write your own consistent hashing solution from scratch, it's important that you
are aware of consistent hashing, so that you can ensure it's enabled in your client. For
many libraries, it's still not the default behavior, even when supported by the library.

Auto Discovery only works for Memcached, not Redis. When ElastiCache repairs or
replaces a cache node, the Domain Name Service (DNS) name of the cache node will
remain the same, meaning your application doesn't need to use Auto Discovery to deal
with common failures. You only need Auto Discovery support if you dynamically scale 
Amazon Web Services Performance at Scale with Amazon ElastiCache
the size of your cache cluster on the fly, while your application is running.

The two most interesting events that ElastiCache publishes, at least for the purposes of
scaling our cache, are ElastiCache:AddCacheNodeComplete and
ElastiCache:RemoveCacheNodeComplete. These events are published when cache
nodes are added or removed from the cluster. By listening for these events, your
application can dynamically reconfigure itself to detect the new cache nodes.

### More Caching Strategies

Also known as dog piling, the thundering herd effect is what happens when many
different application processes simultaneously request a cache key, get a cache miss,
and then each hits the same database query in parallel.

TTLs aside, this effect is also common when adding a new cache node, because the
new cache node's memory is empty. In both cases, the solution is to prewarm the cache
by following these steps:

Finally, there is one last subtle side effect of using TTLs everywhere. If you use the
same TTL length (say 60 minutes) consistently, then many of your cache keys might
expire within the same time window, even after prewarming your cache. One strategy
that's easy to implement is to add some randomness to your TTL

### MISC

Amazon ElastiCache does not currently support using Auto Scaling to scale the number
of cache nodes in a cluster. To change the number of cache nodes, you can use either
the AWS Management Console or the AWS API to modify the cluster.

## Exercises

### Create Redis (Not Cluster-Mode)

1. Create Redis; Name: hello-redis

2. Create EC2 in same security group

3. Install Redis CLI

4. Connect to Redis primary endpoint and interact

#### Supplemental Tasks

1. Delete EC2 Instance

2. Delete Redis Cluster
