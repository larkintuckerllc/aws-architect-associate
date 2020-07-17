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

## Exercises

### Create Table

1. Create Table; Name: Todos; PK: IdentityId; SK: Id

2. Create Item; IdentityId: John; Id: a; Name: Apple

3. Create Item; IdentityId: Suzy; Id: a; Name: Alaska

4. Scan Table; observe all items

5. Query Table; observe all items with PK

### TODO

TODO

#### Supplemental Tasks

TODO
