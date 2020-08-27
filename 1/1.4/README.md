# 1.4 Choose appropriate resilient storage

* [Amazon Elastic Block Store (EBS)](ebs)

* [Amazon Elastic File System (EFS)](efs)

* [Amazon Simple Storage System (S3)](s3)

* [AWS Snow Family](snow)

* [Amazon Glacier](glacier)

* AWS DataSync: AWS DataSync is an online data transfer service that simplifies, automates, and accelerates copying large amounts of data to and from AWS storage services over the internet or AWS Direct Connect. DataSync can copy data between Network File System (NFS), Server Message Block (SMB) file servers, self-managed object storage, or AWS Snowcone, and Amazon Simple Storage Service (Amazon S3) buckets, Amazon EFS file systems, and Amazon FSx for Windows File Server file systems.

* AWS Storage Gateway: AWS Storage Gateway connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure. You can use the service to store data in the AWS Cloud for scalable and cost-effective storage that helps maintain data security.

File Gateway – A file gateway supports a file interface into Amazon Simple Storage Service (Amazon S3) and combines a service and a virtual software appliance. By using this combination, you can store and retrieve objects in Amazon S3 using industry-standard file protocols such as Network File System (NFS) and Server Message Block (SMB).

Volume Gateway – A volume gateway provides cloud-backed storage volumes that you can mount as Internet Small Computer System Interface (iSCSI) devices from your on-premises application servers.

**note:** A Cloud Guru; AKA. Gateway-Stored Volumes

The Volume Gateway supports the following volume configurations:

Cached volumes – You store your data in Amazon Simple Storage Service (Amazon S3) and retain a copy of frequently accessed data subsets locally.

Stored volumes – If you need low-latency access to your entire dataset, first configure your on-premises gateway to store all your data locally. Then asynchronously back up point-in-time snapshots of this data to Amazon S3.

Tape Gateway – A tape gateway provides cloud-backed virtual tape storage. The tape gateway is deployed into your on-premises environment as a VM running on VMware ESXi, KVM, or Microsoft Hyper-V hypervisor.

**note:** A Cloud Guru, has support for bandwidth throttling; so will not crush a remote office.

* Amazon Athena: Amazon Athena is an interactive query service that makes it easy to analyze data directly in Amazon Simple Storage Service (Amazon S3) using standard SQL. With a few actions in the AWS Management Console, you can point Athena at your data stored in Amazon S3 and begin using standard SQL to run ad-hoc queries and get results in seconds.

**note:** Use case is to use CloudTrail to log events into S3.  Then use Athena to query. General pattern is to create a "database", define a schema for a table and point to a S3 bucket.

**note**: A Cloud Guru, file in Parquet format for performance.

* Amazon Macie: Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover, monitor, and help you protect your sensitive data in Amazon Simple Storage Service (Amazon S3). Macie automates the discovery of sensitive data, such as personally identifiable information (PII) and intellectual property, to provide you with a better understanding of the data that your organization stores in Amazon S3.

* Amazon Elastic Transcoder lets you convert media files that you have stored in Amazon Simple Storage Service (Amazon S3) into media files in the formats required by consumer playback devices. For example, you can convert large, high-quality digital media files into formats that users can play back on mobile devices, tablets, web browsers, and connected televisions.

* Amazon WorkDocs is a fully managed, secure enterprise storage and sharing service with strong administrative controls and feedback capabilities that improve user productivity. Files are stored in the cloud, safely and securely. Your files are only visible to you, and your designated contributors and viewers. Other members of your organization do not have access to any of your files unless you specifically grant them access.
