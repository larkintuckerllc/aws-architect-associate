# 1.3 Design decoupling mechanisms using AWS services

* [Amazon Simple Queue Service](sqs)

* [Amazon Simple Notification Service](sns)

* Amazon Kinesis Data Streams: You can use Amazon Kinesis Data Streams to collect and process large streams of data records in real time. Kinesis Data Streams is part of the Kinesis streaming data platform, along with Kinesis Data Firehose, Kinesis Video Streams, and Kinesis Data Analytics.

**note:** A Cloud Guru. Each shard can process 1000 msgs / second. Limit is 500 shards

**note:** Data consists of a partition key, sequence number, and blob (less than 1 MB)

Kinesis Streams: Stream data from Producers stored in Shards from 1 - 7 Days.  Can be read by Consumer to do something. Default 1 day.

Kinesis Data Firehose: Amazon Kinesis Data Firehose is a fully managed service for delivering real-time streaming data to destinations such as Amazon Simple Storage Service (Amazon S3), Amazon Redshift, Amazon Elasticsearch Service (Amazon ES), Splunk, and any custom HTTP endpoint or HTTP endpoints owned by supported third-party service providers, including Datadog, MongoDB, and New Relic.

Kinesis Data Analytics: Works with either Streams or Firehose and does analysis.

* Amazon MQ: Amazon MQ is a managed message broker service for Apache ActiveMQ that makes it easy to migrate to a message broker in the cloud. A message broker allows software applications and components to communicate using various programming languages, operating systems, and formal messaging protocols.

* Amazon SWF: The Amazon Simple Workflow Service (Amazon SWF) makes it easy to build applications that coordinate work across distributed components. In Amazon SWF, a task represents a logical unit of work that is performed by a component of your application. Coordinating tasks across the application involves managing intertask dependencies, scheduling, and concurrency in accordance with the logical flow of the application.

**note:** A Cloud Guru, can involve human task, e.g., Amazon warehouse. Includes, Workflow Starters, Deciders, and Activity Workers
