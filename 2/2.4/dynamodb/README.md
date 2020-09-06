# Amazon DynamoDb

## Concepts

### Overview

> Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.

&nbsp;

> DynamoDB automatically spreads the data and traffic for your tables over a sufficient number of servers to handle your throughput and storage requirements, while maintaining consistent and fast performance. All of your data is stored on solid-state disks (SSDs) and is automatically replicated across multiple Availability Zones in an AWS Region, providing built-in high availability and data durability.

-AWS-[What Is Amazon DynamoDB?](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)

> Tables – Similar to other database systems, DynamoDB stores data in tables.

&nbsp;

> Items – Each table contains zero or more items. An item is a group of attributes that is uniquely identifiable among all of the other items.

**note:** A Cloud Guru, items less than 500 KB

&nbsp;

> Attributes – Each item is composed of one or more attributes. An attribute is a fundamental data element, something that does not need to be broken down any further.

&nbsp;

> Primary Key: When you create a table, in addition to the table name, you must specify the primary key of the table. The primary key uniquely identifies each item in the table, so that no two items can have the same key.

&nbsp;

> DynamoDB supports two different kinds of primary keys:

* Partition key – A simple primary key, composed of one attribute known as the partition key.

* Partition key and sort key – Referred to as a composite primary key, this type of key is composed of two attributes. The first attribute is the partition key, and the second attribute is the sort key.

> Each primary key attribute must be a scalar (meaning that it can hold only a single value). The only data types allowed for primary key attributes are string, number, or binary. There are no such restrictions for other, non-key attributes.

&nbsp;

> You can create one or more secondary indexes on a table. A secondary index lets you query the data in the table using an alternate key, in addition to queries against the primary key.

&nbsp;

> DynamoDB supports two kinds of indexes:

* Global secondary index – An index with a partition key and sort key that can be different from those on the table.

* Local secondary index – An index that has the same partition key as the table, but a different sort key.

> Each table in DynamoDB has a quota of 20 global secondary indexes (default quota) and 5 local secondary indexes per table.

In a DynamoDB table, each key value must be unique. However, the key values in a global secondary index do not need to be unique.

A projection is the set of attributes that is copied from a table into a secondary index. The partition key and sort key of the table are always projected into the index; you can project other attributes to support your application's query requirements. When you query an index, Amazon DynamoDB can access any attribute in the projection as if those attributes were in a table of their own.

DynamoDB automatically synchronizes each global secondary index with its base table. When an application writes or deletes items in a table, any global secondary indexes on that table are updated asynchronously, using an eventually consistent model.

A table with many global secondary indexes incurs higher costs for write activity than tables with fewer indexes

When you create a global secondary index on a provisioned mode table, you must specify read and write capacity units for the expected workload on that index. The provisioned throughput settings of a global secondary index are separate from those of its base table. A Query operation on a global secondary index consumes read capacity units from the index, not the base table. When you put, update or delete items in a table, the global secondary indexes on that table are also updated. These index updates consume write capacity units from the index, not from the base table.

**note:** Can use Global Secondary index to create clone of table with different capacity (for different customers)

&nbsp;

> DynamoDB Streams is an optional feature that captures data modification events in DynamoDB tables. The data about these events appear in the stream in near-real time, and in the order that the events occurred.

&nbsp;

> You can use DynamoDB Streams together with AWS Lambda to create a trigger—code that executes automatically whenever an event of interest appears in a stream.

-AWS-[Core Components of Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.CoreComponents.html)

### API (Selected)

> PutItem – Writes a single item to a table. You must specify the primary key attributes, but you don't have to specify other attributes.

&nbsp;

> BatchWriteItem – Writes up to 25 items to a table.

&nbsp;

> GetItem – Retrieves a single item from a table. You must specify the primary key for the item that you want. You can retrieve the entire item, or just a subset of its attributes.

&nbsp;

> BatchGetItem – Retrieves up to 100 items from one or more tables.

&nbsp;

> Query – Retrieves all items that have a specific partition key. You must specify the partition key value. You can retrieve entire items, or just a subset of their attributes. Optionally, you can apply a condition to the sort key values so that you only retrieve a subset of the data that has the same partition key. You can use this operation on a table, provided that the table has both a partition key and a sort key. You can also use this operation on an index, provided that the index has both a partition key and a sort key.

&nbsp;

> Scan – Retrieves all items in the specified table or index. You can retrieve entire items, or just a subset of their attributes. Optionally, you can apply a filtering condition to return only the values that you are interested in and discard the rest.

&nbsp;

> UpdateItem – Modifies one or more attributes in an item. You must specify the primary key for the item that you want to modify. You can add new attributes and modify or remove existing attributes

&nbsp;

> DeleteItem – Deletes a single item from a table. You must specify the primary key for the item that you want to delete.

&nbsp;

> BatchWriteItem – Deletes up to 25 items from one or more tables.

-AWS-[DynamoDB API](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.API.html)

> DynamoDB supports eventually consistent and strongly consistent reads.

* Eventually Consistent Reads: When you read data from a DynamoDB table, the response might not reflect the results of a recently completed write operation.

* Strongly Consistent Reads: When you request a strongly consistent read, DynamoDB returns a response with the most up-to-date data, reflecting the updates from all prior write operations that were successful.

-AWS-[Read Consistency](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html)

### Performance

> Amazon DynamoDB has two read/write capacity modes for processing reads and writes on your tables:

* On-demand

* Provisioned (default, free-tier eligible)

> The read/write capacity mode controls how you are charged for read and write throughput and how you manage capacity. You can set the read/write capacity mode when creating a table or you can change it later.

&nbsp;

> When you choose on-demand mode, DynamoDB instantly accommodates your workloads as they ramp up or down to any previously reached traffic level. If a workload’s traffic level hits a new peak, DynamoDB adapts rapidly to accommodate the workload.

&nbsp;

> One read request unit represents one strongly consistent read request, or two eventually consistent read requests, for an item up to 4 KB in size. Transactional read requests require 2 read request units to perform one read for items up to 4 KB. If you need to read an item that is larger than 4 KB, DynamoDB needs additional read request units.

&nbsp;

> One write request unit represents one write for an item up to 1 KB in size. If you need to write an item that is larger than 1 KB, DynamoDB needs to consume additional write request units. Transactional write requests require 2 write request units to perform one write for items up to 1 KB.

&nbsp;

> If you choose provisioned mode, you specify the number of reads and writes per second that you require for your application.

&nbsp;

> Throttling prevents your application from consuming too many capacity units. When a request is throttled, it fails with an HTTP 400 code (Bad Request) and a ProvisionedThroughputExceededException.

&nbsp;

> DynamoDB auto scaling actively manages throughput capacity for tables and global secondary indexes. With auto scaling, you define a range (upper and lower limits) for read and write capacity units. You also define a target utilization percentage within that range. DynamoDB auto scaling seeks to maintain your target utilization, even as your application workload increases or decreases.

&nbsp;

> As a DynamoDB customer, you can purchase reserved capacity in advance, as described at Amazon DynamoDB Pricing. With reserved capacity, you pay a one-time upfront fee and commit to a minimum provisioned usage level over a period of time. Your reserved capacity is billed at the hourly reserved capacity rate. By reserving your read and write capacity units ahead of time, you realize significant cost savings compared to on-demand provisioned throughput settings.

-AWS-[Read/Write Capacity Mode](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)

### On-Demand Backup

> You can use the on-demand backup feature to create full backups of your Amazon DynamoDB tables.

&nbsp;

> When you create an on-demand backup, a time marker of the request is cataloged. The backup is created asynchronously by applying all changes until the time of the request to the last full table snapshot. Backup requests are processed instantaneously and become available for restore within minutes.

&nbsp;

> All backups in DynamoDB work without consuming any provisioned throughput on the table.

&nbsp;

> `If you don't want to create scheduling scripts and cleanup jobs, you can use AWS Backup to create backup plans with schedules and retention policies for your DynamoDB tables.

&nbsp;

> You restore a table without consuming any provisioned throughput on the table. You can do a full table restore from your DynamoDB backup, or you can configure the destination table settings. When you do a restore, you can change the following table settings:

* Global secondary indexes (GSIs)

* Local secondary indexes (LSIs)

* Billing mode

* Provisioned read and write capacity

* Encryption settings

> You can also restore your DynamoDB table data across AWS Regions such that the restored table is created in a different Region from where the backup resides.

&nbsp;

> You must manually set up the following on the restored table:

Number of ancillary things like IAM.

-AWS-[Back Up and Restore DynamoDB Tables: How It Works](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/backuprestore_HowItWorks.html)

### Point-in-Time Recovery

> Amazon DynamoDB point-in-time recovery (PITR) provides automatic backups of your DynamoDB table data.

&nbsp;

> You can enable point-in-time recovery using the AWS Management Console, AWS Command Line Interface (AWS CLI), or the DynamoDB API.

&nbsp;

> After you enable point-in-time recovery, you can restore to any point in time within EarliestRestorableDateTime and LatestRestorableDateTime. LatestRestorableDateTime is typically 5 minutes before the current time.

&nbsp;

> For EarliestRestorableDateTime, you can restore your table to any point in time during the last 35 days. The retention period is a fixed 35 days (5 calendar weeks) and can't be modified.

-AWS-[Point-in-Time Recovery: How It Works](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/PointInTimeRecovery_Howitworks.html)

### Misc

> Amazon DynamoDB global tables provide a fully managed solution for deploying a multiregion, multi-master database, without having to build and maintain your own replication solution. With global tables you can specify the AWS Regions where you want the table to be available. DynamoDB performs all of the necessary tasks to create identical tables in these Regions and propagate ongoing data changes to all of them.

-AWS-[Global Tables: Multi-Region Replication with DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GlobalTables.html)

> With Amazon DynamoDB transactions, you can group multiple actions together and submit them as a single all-or-nothing TransactWriteItems or TransactGetItems operation.

-AWS-[Amazon DynamoDB Transactions: How It Works](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/transaction-apis.html)

> Amazon DynamoDB Accelerator (DAX) is designed to run within an Amazon Virtual Private Cloud (Amazon VPC) environment.

&nbsp;

> To create a DAX cluster, you use the AWS Management Console. Unless you specify otherwise, your DAX cluster runs within your default VPC. To run your application, you launch an Amazon EC2 instance into your Amazon VPC. You then deploy your application (with the DAX client) on the EC2 instance.

&nbsp;

> At runtime, the DAX client directs all of your application's DynamoDB API requests to the DAX cluster. If DAX can process one of these API requests directly, it does so. Otherwise, it passes the request through to DynamoDB.

&nbsp;

> If the request specifies eventually consistent reads (the default behavior), it tries to read the item from DAX:

&nbsp;

> With these operations, data is first written to the DynamoDB table, and then to the DAX cluster. The operation is successful only if the data is successfully written to both the table and to DAX.

&nbsp;

> The item cache has a Time to Live (TTL) setting, which is 5 minutes by default. DAX assigns a timestamp to every item that it writes to the item cache. An item expires if it has remained in the cache for longer than the TTL setting.

&nbsp;

> DAX also maintains a query cache to store the results from Query and Scan operations. The items in this cache represent result sets from queries and scans on DynamoDB tables. These result sets are stored by their parameter values.

&nbsp;

You can specify the TTL setting for the query cache when you create a new DAX cluster.

-AWS-[In-Memory Acceleration with DynamoDB Accelerator (DAX)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAX.html)

> NoSQL Workbench for Amazon DynamoDB is a cross-platform client-side application for modern database development and operations and is available for Windows and macOS. NoSQL Workbench is a unified visual tool that provides data modeling, data visualization, and query development features to help you design, create, query, and manage DynamoDB tables.

-AWS-[NoSQL Workbench for Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/workbench.html)

> When enabling TTL on a DynamoDB table, you must identify a specific attribute name that the service will look for when determining if an item is eligible for expiration. After you enable TTL on a table, a per-partition scanner background process automatically and continuously evaluates the expiry status of items in the table.

&nbsp;

> The scanner background process compares the current time, in Unix epoch time format in seconds, to the value stored in the user-defined attribute of an item.

-AWS-[How It Works: DynamoDB Time to Live (TTL)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/howitworks-ttl.html)

### Multi-Tenancy

Silo: Might consider still using a single Tables with IAM Policies, otherwise use prefixs to name Tables

Bridge: Essentially same as Silo

Pool: 

### Partitions (Under Hood)

DynamoDB creates partions using a hash of the partition key.  The number of partitions is based on both R/W units and size.

RCU / 3000 + WCU / 1000
Data Size / 10 GB

and then Max

Then divides up RCU and WCU across all partitions. So pick partition key to spead load.

## Exercises

### Create Table

1. Create Table; Name: Todos; PK: IdentityId; SK: Id

2. Create Item; IdentityId: John; Id: a; Name: Apple

3. Create Item; IdentityId: Suzy; Id: a; Name: Alaska

4. Scan Table; observe all items

5. Query Table; observe all items with PK

#### Supplemental Tasks

1. Delete Todos table
