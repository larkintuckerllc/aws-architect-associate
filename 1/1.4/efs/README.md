# Amazon Elastic File System (EFS)

## Concepts

### Overview

> Amazon Elastic File System (Amazon EFS) provides a simple, scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources. It is built to scale on demand to petabytes without disrupting applications, growing and shrinking automatically as you add and remove files, eliminating the need to provision and manage capacity to accommodate growth.

&nbsp;

> Amazon EFS supports the Network File System version 4 (NFSv4.1 and NFSv4.0) protocol, so the applications and tools that you use today work seamlessly with Amazon EFS. Multiple Amazon EC2 instances can access an Amazon EFS file system at the same time, providing a common data source for workloads and applications running on more than one instance or server.

&nbsp;

> The service is designed to be highly scalable, highly available, and highly durable. Amazon EFS file systems store data and metadata across multiple Availability Zones in an AWS Region.

&nbsp;

> Amazon EFS supports two forms of encryption for file systems, encryption in transit and encryption at rest. You can enable encryption at rest when creating an Amazon EFS file system. If you do, all your data and metadata is encrypted. You can enable encryption in transit when you mount the file system.

-AWS-[What Is Amazon Elastic File System?](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)

### EFS Storage Classes

> Amazon EFS file systems have two storage classes available:

&nbsp;

> Infrequent Access – The Infrequent Access (IA) storage class is a lower-cost storage class that's designed for storing long-lived, infrequently accessed files cost-effectively.

&nbsp;

> Standard – The Standard storage class is used to store frequently accessed files.

-AWS-[EFS Storage Classes](https://docs.aws.amazon.com/efs/latest/ug/storage-classes.html)

> File system operations for lifecycle management, which transition files to IA storage, have a lower priority than operations for EFS file system workloads.

&nbsp;

> Amazon EFS lifecycle management automatically manages cost-effective file storage for your file systems. When enabled, lifecycle management migrates files that have not been accessed for a set period of time to the Infrequent Access (IA) storage class. You define that period of time by using a lifecycle policy.

&nbsp;

> After lifecycle management moves a file into the IA storage class, the file remains there indefinitely.

&nbsp;

> You can specify one of four lifecycle policies for your Amazon EFS file system, as follows:

* AFTER_7_DAYS

* AFTER_14_DAYS

* AFTER_30_DAYS

* AFTER_60_DAYS

* AFTER_90_DAYS

-AWS-[EFS Lifecycle Management](https://docs.aws.amazon.com/efs/latest/ug/lifecycle-management-efs.html)

### Performance Characteristics

> We recommend the General Purpose performance mode for the majority of your Amazon EFS file systems. General Purpose is ideal for latency-sensitive use cases, like web serving environments, content management systems, home directories, and general file serving.

&nbsp;

> File systems in the Max I/O mode can scale to higher levels of aggregate throughput and operations per second. This scaling is done with a tradeoff of slightly higher latencies for file metadata operations. Highly parallelized applications and workloads, such as big data analysis, media processing, and genomics analysis, can benefit from this mode.

&nbsp;

> To move to a different performance mode, migrate the data to a different file system that was created in the other performance mode.

&nbsp;

> There are two throughput modes to choose from for your file system, Bursting Throughput and Provisioned Throughput. With Bursting Throughput mode, throughput on Amazon EFS scales as the size of your file system in the standard storage class grows.

-AWS-[Amazon EFS Performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html#performancemodes)

### Bursting Throughput Mode

> All file systems, regardless of size, can burst to 100 MiB/s of throughput. Those over 1 TiB in the standard storage class can burst to 100 MiB/s per TiB of data stored in the file system.

&nbsp;

> Amazon EFS uses a credit system to determine when file systems can burst. Each file system earns credits over time at a baseline rate that is determined by the size of the file system that is stored in the standard storage class. A file system uses credits whenever it reads or writes data. The baseline rate is 50 MiB/s per TiB of storage (equivalently, 50 KiB/s per GiB of storage).

&nbsp;

> The bursting capability (both in terms of length of time and burst rate) of a file system is directly related to its size. Larger file systems can burst at larger rates for longer periods of time. In some cases, your application might need to burst more (that is, you might find that your file system is running out of burst credits. In these cases, you should increase the size of your file system, or switch to Provisioned Throughput mode.

-AWS-[Amazon EFS Performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html#performancemodes)

### Provisioned Throughput Mode

> Provisioned Throughput mode is available for applications with high throughput to storage (MiB/s per TiB) ratios, or with requirements greater than those allowed by the Bursting Throughput mode.

&nbsp;

> Additional charges are associated with using Provisioned Throughput mode. Using Provisioned Throughput mode, you're billed for the storage that you use and for the throughput that you provision above what you're provided. The amount of throughput that you are provided is based on the amount of data stored in the Standard storage class.

&nbsp;

> If your file system is in the Provisioned Throughput mode, you can increase the Provisioned Throughput of your file system as often as you want. You can decrease your file system throughput in Provisioned Throughput mode as long as it's been more than 24 hours since the last decrease. Additionally, you can change between Provisioned Throughput mode and the default Bursting Throughput mode as long as it’s been more than 24 hours since the last throughput mode change.

-AWS-[Amazon EFS Performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html#performancemodes)

## Exercises
