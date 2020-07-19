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

## MemCache

> The Memcached engine supports Auto Discovery. Auto Discovery is the ability for client programs to automatically identify all of the nodes in a cache cluster, and to initiate and maintain connections to all of these nodes. With Auto Discovery, your application doesn't need to manually connect to individual nodes. Instead, your application connects to a configuration endpoint.

&nbsp;

> When you run the Memcached engine, clusters can be made up of 1–20 nodes. You partition your database across the nodes. Your application reads and writes to each node's endpoint.
