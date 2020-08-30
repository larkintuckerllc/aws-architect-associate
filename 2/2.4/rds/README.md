# Amazon Relational Database Service (RDS)

## Concepts

### Overview

> Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks.

&nbsp;

> The basic building block of Amazon RDS is the DB instance. A DB instance is an isolated database environment in the AWS Cloud. Your DB instance can contain multiple user-created databases. You can access your DB instance by using the same tools and applications that you use with a standalone database instance.

&nbsp;

> Each DB instance runs a DB engine. Amazon RDS currently supports the MySQL, MariaDB, PostgreSQL, Oracle, and Microsoft SQL Server DB engines.

&nbsp;

> You can have up to 40 Amazon RDS DB instances, with the following limitations:

&nbsp;

> 10 for each SQL Server edition (Enterprise, Standard, Web, and Express) under the "license-included" model

&nbsp;

> 10 for Oracle under the "license-included" model

&nbsp;

> Each DB instance has a DB instance identifier. This customer-supplied name uniquely identifies the DB instance when interacting with the Amazon RDS API and AWS CLI commands. The DB instance identifier must be unique for that customer in an AWS Region.

&nbsp;

> The identifier is used as part of the DNS hostname allocated to your instance by RDS.

&nbsp;

> Amazon RDS creates a master user account for your DB instance as part of the creation process. This master user has permissions to create databases and to perform create, delete, select, update, and insert operations on tables the master user creates.

-AWS-[Amazon RDS DB Instances](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.DBInstance.html)

**note:** A Cloud Guru: CLI aws rds describe-db-instances

**note:** A Cloud Guru: Since run on EBS, same rules about having to create Snapshot to encrypt; i.e., cannot encrypt on fly. Then copy (can be different Region) to encrypt.

**note:** To share encrypted snapshot with another account; must use custom KMS key to share with another account. Cannot be public, or proprietry.

**note:** RDS has a concept of maintainence window (much like other managed instances, e.g., Redshift)

Can set minors to automatic, majors are always manual. AWS can deprecate with notice 3 minor- 6 month major.

### DB Instance Classes

> Amazon RDS supports three types of instance classes: Standard, Memory Optimized, and Burstable Performance.

&nbsp;

> You can change the CPU and memory available to a DB instance by changing its DB instance class.

&nbsp;

> Some instance classes require that your DB instance is in a VPC.

-AWS-[DB Instance Classes](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.DBInstanceClass.html)

T: Burstable: Variable Workloads Small
M: General Purpose: More CPU
R: Memory: High Memory

### DB Instance Storage

> DB instances for Amazon RDS for MySQL, MariaDB, PostgreSQL, Oracle, and Microsoft SQL Server use Amazon Elastic Block Store (Amazon EBS) volumes for database and log storage. Depending on the amount of storage requested, Amazon RDS automatically stripes across multiple Amazon EBS volumes to enhance performance.

&nbsp;

> General Purpose SSD – General Purpose SSD volumes offer cost-effective storage that is ideal for a broad range of workloads. These volumes deliver single-digit millisecond latencies and the ability to burst to 3,000 IOPS for extended periods of time. Baseline performance for these volumes is determined by the volume's size.

&nbsp;

> Provisioned IOPS – Provisioned IOPS storage is designed to meet the needs of I/O-intensive workloads, particularly database workloads, that require low I/O latency and consistent I/O throughput.

&nbsp;

> Magnetic – Amazon RDS also supports magnetic storage for backward compatibility. We recommend that you use General Purpose SSD or Provisioned IOPS for any new storage needs. The maximum amount of storage allowed for DB instances on magnetic storage is less than that of the other storage types. For more information, see Magnetic Storage.

&nbsp;

> Amazon RDS provides several metrics that you can use to determine how your DB instance is performing. You can view the metrics on the summary page for your instance in Amazon RDS Management Console. You can also use Amazon CloudWatch to monitor these metrics

**note:** There is something called "Enhanced Monitoring" with extra metrics and frequency down to 1 second.

* IOPS – The number of I/O operations completed each second. This metric is reported as the average IOPS for a given time interval. Amazon RDS reports read and write IOPS separately on 1-minute intervals. Total IOPS is the sum of the read and write IOPS.

* Latency – The elapsed time between the submission of an I/O request and its completion. This metric is reported as the average latency for a given time interval. Amazon RDS reports read and write latency separately on 1-minute intervals in units of seconds.

* Throughput – The number of bytes each second that are transferred to or from disk. This metric is reported as the average throughput for a given time interval. Amazon RDS reports read and write throughput separately on 1-minute intervals using units of megabytes per second (MB/s).

* Queue Depth – The number of I/O requests in the queue waiting to be serviced. These are I/O requests that have been submitted by the application but have not been sent to the device because the device is busy servicing other I/O requests. Time spent waiting in the queue is a component of latency and service time (not available as a metric). This metric is reported as the average queue depth for a given time interval. Amazon RDS reports queue depth in 1-minute intervals.

-AWS-[Amazon RDS DB Instance Storage](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html)

> If your workload is unpredictable, you can enable storage autoscaling for an Amazon RDS DB instance. To do so, you can use the Amazon RDS console, the Amazon RDS API, or the AWS CLI.

&nbsp;

> The maximum storage threshold is the limit to which the DB instance can be autoscaled. You can't set the maximum storage threshold for autoscaling-enabled instances to a value greater than the maximum allocated storage.

-AWS-[Working with Storage for Amazon RDS DB Instances](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTypes.html#USER_PIOPS.Autoscaling)

### VPC

> Unless you are working with a legacy DB instance, your DB instance is in a virtual private cloud (VPC). A VPC is a virtual network that is logically isolated from other virtual networks in the AWS Cloud. Amazon VPC lets you launch AWS resources, such as an Amazon RDS DB instance or Amazon EC2 instance, into a VPC. The VPC can either be a default VPC that comes with your account or one that you create. All VPCs are associated with your AWS account.

&nbsp;

> A DB subnet group is a collection of subnets (typically private) that you create in a VPC and that you then designate for your DB instances. A DB subnet group allows you to specify a particular VPC when creating DB instances using the CLI or API; if you use the console, you can just choose the VPC and subnets you want to use.

&nbsp;

> Each DB subnet group should have subnets in at least two Availability Zones in a given AWS Region. When creating a DB instance in a VPC, you must choose a DB subnet group. Amazon RDS uses that DB subnet group and your preferred Availability Zone to choose a subnet and an IP address within that subnet to associate with your DB instance.

-AWS-[Working with a DB Instance in a VPC](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html)

### High Availablity (Multi-AZ)

> Amazon RDS provides high availability and failover support for DB instances using Multi-AZ deployments. Amazon RDS uses several different technologies to provide failover support. Multi-AZ deployments for MariaDB, MySQL, Oracle, and PostgreSQL DB instances use Amazon's failover technology. SQL Server DB instances use SQL Server Database Mirroring (DBM) or Always On Availability Groups (AGs).

&nbsp;

> In a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone. The primary DB instance is synchronously replicated across Availability Zones to a standby replica to provide data redundancy, eliminate I/O freezes, and minimize latency spikes during system backups.

&nbsp;

> Using the RDS console, you can create a Multi-AZ deployment by simply specifying Multi-AZ when creating a DB instance. You can use the console to convert existing DB instances to Multi-AZ deployments by modifying the DB instance and specifying the Multi-AZ option.

&nbsp;

> DB instances using Multi-AZ deployments can have increased write and commit latency compared to a Single-AZ deployment, due to the synchronous data replication that occurs. 

&nbsp;

> In the event of a planned or unplanned outage of your DB instance, Amazon RDS automatically switches to a standby replica in another Availability Zone if you have enabled Multi-AZ. The time it takes for the failover to complete depends on the database activity and other conditions at the time the primary DB instance became unavailable. Failover times are typically 60–120 seconds.

&nbsp;

> The failover mechanism automatically changes the Domain Name System (DNS) record of the DB instance to point to the standby DB instance.

&nbsp;

> Because AWS resources use DNS name entries that occasionally change, we recommend that you configure your JVM with a TTL value of no more than 60 seconds. 

-AWS-[High Availability (Multi-AZ) for Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)

**note:** A Cloud Guru: Backend are restores use backup. You can force failover by rebooting.

### Read Replicas

> Amazon RDS uses the MariaDB, MySQL, Oracle, PostgreSQL, and Microsoft SQL Server DB engines' built-in replication functionality to create a special type of DB instance called a read replica from a source DB instance. Updates made to the source DB instance are asynchronously copied to the read replica. You can reduce the load on your source DB instance by routing read queries from your applications to the read replica. Using read replicas, you can elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads.

&nbsp;

> When you create a read replica, you first specify an existing DB instance as the source. Then Amazon RDS takes a snapshot of the source instance and creates a read-only instance from the snapshot. Amazon RDS then uses the asynchronous replication method for the DB engine to update the read replica whenever there is a change to the source DB instance. The read replica operates as a DB instance that allows only read-only connections. Applications connect to a read replica the same way they do to any DB instance. Amazon RDS replicates all databases in the source DB instance.

&nbsp;

> When creating a read replica, there are a few things to consider. First, you must enable automatic backups on the source DB instance by setting the backup retention period to a value other than 0. This requirement also applies to a read replica that is the source DB instance for another read replica. 

&nbsp;

> You can promote a MySQL, MariaDB, Oracle, PostgreSQL, or SQL Server read replica into a standalone DB instance. When you promote a read replica, the DB instance is rebooted before it becomes available.

&nbsp;

> With Amazon RDS, you can create a MariaDB, MySQL, Oracle, or PostgreSQL read replica in a different AWS Region than the source DB instance. Creating a cross-Region read replica isn't supported for SQL Server on Amazon RDS.

&nbsp;

> The data transferred for cross-Region replication incurs Amazon RDS data transfer charges. 

-AWS-[Working with Read Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)

**note:** A Cloud Guru: Up to 5 RR. Key Metric: Replica Lag

### Backups

> Amazon RDS creates and saves automated backups of your DB instance during the backup window of your DB instance. RDS creates a storage volume snapshot of your DB instance, backing up the entire DB instance and not just individual databases. RDS saves the automated backups of your DB instance according to the backup retention period that you specify. If necessary, you can recover your database to any point in time during the backup retention period.

&nbsp;

> Your Amazon RDS backup storage for each region is composed of the automated backups and manual DB snapshots for that region. Total backup storage space equals the sum of the storage for all backups in that region. Moving a DB snapshot to another region increases the backup storage in the destination region. Backups are stored in Amazon S3.

&nbsp;

> You can set the backup retention period when you create a DB instance. If you don't set the backup retention period, the default backup retention period is one day if you create the DB instance using the Amazon RDS API or the AWS CLI. The default backup retention period is seven days if you create the DB instance using the console. After you create a DB instance, you can modify the backup retention period. You can set the backup retention period to between 0 and 35 days. Setting the backup retention period to 0 disables automated backups. Manual snapshot limits (100 per region) do not apply to automated backups.

**note:** Default 7 days.

-AWS-[Working With Backups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html)

> Amazon RDS creates a storage volume snapshot of your DB instance, backing up the entire DB instance and not just individual databases. Creating this DB snapshot on a Single-AZ DB instance results in a brief I/O suspension that can last from a few seconds to a few minutes, depending on the size and class of your DB instance.

-AWS-[Creating a DB Snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html)

Amazon RDS creates a storage volume snapshot of your DB instance, backing up the entire DB instance and not just individual databases. You can create a DB instance by restoring from this DB snapshot. When you restore the DB instance, you provide the name of the DB snapshot to restore from, and then provide a name for the new DB instance that is created from the restore. You can't restore from a DB snapshot to an existing DB instance; a new DB instance is created when you restore.

-AWS-[Restoring from a DB Snapshot](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_RestoreFromSnapshot.html)

### Misc

Instance class scaling requires downtime.

Disk scaling does not; first scaling takes a bit of effort. Cannot scale more than 1 per 6 hours.

## Exercises

### Create Single RDS Instance

1. Standard Create

2. PostgreSQL

3. Free Tier

4. Password

5. Disable: Autoscaling

6. my-security-group (but need to allow all traffic between instances in same SG)

7. Pick AZ

8. Create EC2 Instance

9. upgrade

10. Install pgclient

11. Connect to Database

#### Supplemental Tasks

1. Delete both EC2 and RDS instance
