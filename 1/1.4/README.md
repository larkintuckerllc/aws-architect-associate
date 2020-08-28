# 1.4 Choose appropriate resilient storage

* [Amazon Elastic Block Store (EBS)](ebs)

* [Amazon Elastic File System (EFS)](efs)

* [Amazon Simple Storage System (S3)](s3)

* [AWS Snow Family](snow)

* [Amazon Glacier](glacier)

* Amazon EC2 instance store volumes (also called ephemeral drives) provide temporary block-level storage for many EC2 instance types. This storage consists of a preconfigured and pre-attached block of disk storage on the same physical server that hosts the EC2 instance for which the block provides storage.

AWS offers two EC2 instance families that are purposely built for storage-centric
workloads. Performance specifications of the storage-optimized (i2) and densestorage (d2) instance families are outlined in the following table

i2: SSD (365K IOPS Read)
d2  HDD (3.5 GiB/s Read)

Note that applications using instance storage for persistent data generally provide data durability through replication, or by periodically copying data to durable storage.

**note:** No Snapshots, No Encryption (do self)

* AWS DataSync: AWS DataSync is an online data transfer service that simplifies, automates, and accelerates copying large amounts of data to and from AWS storage services over the internet or AWS Direct Connect. DataSync can copy data between Network File System (NFS), Server Message Block (SMB) file servers, self-managed object storage, or AWS Snowcone, and Amazon Simple Storage Service (Amazon S3) buckets, Amazon EFS file systems, and Amazon FSx for Windows File Server file systems.

* AWS Storage Gateway: AWS Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure. You can use the service to store data in the AWS Cloud for scalable and cost-effective storage that helps maintain data security.

File Gateway – A file gateway supports a file interface into Amazon Simple Storage Service (Amazon S3) and combines a service and a virtual software appliance. By using this combination, you can store and retrieve objects in Amazon S3 using industry-standard file protocols such as Network File System (NFS) and Server Message Block (SMB).

Files written to a file share become objects in Amazon S3, with the path as the key. There is a one-to-one mapping between files and objects, and the gateway asynchronously updates the objects in Amazon S3 as you change the files. Existing objects in the bucket appear as files in the file system, and the key becomes the path. Objects are encrypted with Amazon S3–server-side encryption keys (SSE-S3). All data transfer is done through HTTPS.

Volume Gateway – A volume gateway provides cloud-backed storage volumes that you can mount as Internet Small Computer System Interface (iSCSI) devices from your on-premises application servers.

**note:** A Cloud Guru; AKA. Gateway-Stored Volumes

The Volume Gateway supports the following volume configurations:

Cached volumes – You store your data in Amazon Simple Storage Service (Amazon S3) and retain a copy of frequently accessed data subsets locally.

All gateway data and snapshot data for cached volumes is stored in Amazon S3 and encrypted at rest using server-side encryption (SSE). However, you can't access this data with the Amazon S3 API or other tools such as the Amazon S3 Management Console.

Stored volumes – If you need low-latency access to your entire dataset, first configure your on-premises gateway to store all your data locally. Then asynchronously back up point-in-time snapshots of this data to Amazon S3.

**note:** Data stored as EBS snapshots

Tape Gateway – A tape gateway provides cloud-backed virtual tape storage. The tape gateway is deployed into your on-premises environment as a VM running on VMware ESXi, KVM, or Microsoft Hyper-V hypervisor.

The AWS Storage Gateway encrypts all data in transit to and from AWS by using SSL. All volume and snapshot data stored in AWS using gateway-stored or gateway-cached volumes and all virtual tape data stored in AWS using a gatewayVTL is encrypted at rest using AES-256, a secure symmetric-key encryption standard using 256-bit encryption keys.

**note:** A Cloud Guru, has support for bandwidth throttling; so will not crush a remote office.

* Amazon Athena: Amazon Athena is an interactive query service that makes it easy to analyze data directly in Amazon Simple Storage Service (Amazon S3) using standard SQL. With a few actions in the AWS Management Console, you can point Athena at your data stored in Amazon S3 and begin using standard SQL to run ad-hoc queries and get results in seconds.

**note:** Use case is to use CloudTrail to log events into S3.  Then use Athena to query. General pattern is to create a "database", define a schema for a table and point to a S3 bucket.

**note**: A Cloud Guru, file in Parquet format for performance.

* Amazon Macie: Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover, monitor, and help you protect your sensitive data in Amazon Simple Storage Service (Amazon S3). Macie automates the discovery of sensitive data, such as personally identifiable information (PII) and intellectual property, to provide you with a better understanding of the data that your organization stores in Amazon S3.

* Amazon Elastic Transcoder lets you convert media files that you have stored in Amazon Simple Storage Service (Amazon S3) into media files in the formats required by consumer playback devices. For example, you can convert large, high-quality digital media files into formats that users can play back on mobile devices, tablets, web browsers, and connected televisions.

* Amazon WorkDocs is a fully managed, secure enterprise storage and sharing service with strong administrative controls and feedback capabilities that improve user productivity. Files are stored in the cloud, safely and securely. Your files are only visible to you, and your designated contributors and viewers. Other members of your organization do not have access to any of your files unless you specifically grant them access.

* Consistency Model: ACID; Atomic, Consistent, Isolated, and Durable

* Consistency Model: BASE; Basic, Soft, and Eventual Consistency
