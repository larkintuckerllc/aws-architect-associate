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

However, if your overall Amazon EFS workload will exceed 7,000 file operations per second per file system, we recommend the files system use Max I/O performance mode. 

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

### Operations

> Instances connect to a file system by using mount targets you create. We recommend creating a mount target in each of your VPC's Availability Zones so that EC2 instances across your VPC can access the file system.

-AWS Console

> Now that you have created a functioning Amazon EFS file system, you can use AWS DataSync to transfer files from an existing file system to Amazon EFS. AWS DataSync is a data transfer service that simplifies, automates, and accelerates moving and replicating data between on-premises storage systems and AWS storage services over the internet or AWS Direct Connect. AWS DataSync can transfer your file data, and also file system metadata such as ownership, time stamps, and access permissions.

-AWS-[Step 3: Transfer Files to Amazon EFS Using AWS DataSync](https://docs.aws.amazon.com/efs/latest/ug/gs-step-four-sync-files.html)

**note**: You also need to specifify a Security Group; need to think about access by the EC2.

> You can configure an Amazon EC2 instance to automatically mount an EFS file system when it reboots in two ways:

&nbsp;

> When you create a new EC2 instance using the Launch Instance Wizard.

&nbsp;

> Update the EC2 /etc/fstab file with an entry for the EFS file system.

-AWS-[Mounting Your Amazon EFS File System Automatically](https://docs.aws.amazon.com/efs/latest/ug/mount-fs-auto-mount-onreboot.html)

> Using the file system's DNS name is your simplest mounting option. The file system DNS name automatically resolves to the mount target’s IP address in the Availability Zone of the connecting Amazon EC2 instance. You can get this DNS name from the console, or if you have the file system ID, you can construct it using the following convention.

 -AWS-[Mounting on Amazon EC2 with a DNS Name](https://docs.aws.amazon.com/efs/latest/ug/mounting-fs-mount-cmd-dns-name.html)

 > The root directory of a file system, upon creation, is owned by and is writable by the root user, so you need to change permissions to add files.

-AWS-[Step 3: Mount the Amazon EFS File System on the EC2 Instance and Test](https://docs.aws.amazon.com/efs/latest/ug/wt1-test.html)

### Securing Client Access

> You can use both IAM identity policies and resource policies to control NFS client access to Amazon EFS resources in a way that is scalable and optimized for cloud environments. Using IAM, you can permit clients to perform specific actions on a file system, including read-only, write, and root access.

&nbsp;

> NFS clients can identify themselves using an IAM role when connecting to an EFS file system. When a client connects to a file system, Amazon EFS evaluates the file system’s IAM resource policy, which is called a file system policy, along with any identity-based IAM policies to determine the appropriate file system access permissions to grant.

&nbsp;

The default EFS file system policy grants full access to any NFS client that can connect to the file system. The default policy is in effect whenever a user-configured file system policy doesn't exist, including at file system creation

-AWS-[Using IAM to Control NFS Access to Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/iam-access-control-nfs-efs.html)

## Exercises

### Create EFS

#### Assumptions

Understand material in [Elastic Cloud Compute (EC2)](../ec2) and completed exercises:

* Create Key Pair [Elastic Cloud Compute (EC2)](../ec2)

* Create Security Group [Elastic Cloud Compute (EC2)](../ec2)

**note**: Need to update *my-security-group* to allow all inbound traffic from same Security Group

#### Tasks

1. Create EFS

Properties;

* All AZ in default VPC

* Security Group: *my-security-group*

### Mount EFS Using NFS Client

1. Create an EC2 instance in default Subnet in default VPC in a Region; properties below

2. Mount / Automount EFS to EC2 using NFS Client (see [documentation](https://docs.aws.amazon.com/efs/latest/ug/wt1-test.html))

3. Unmount EFS from EC2

Properties:

* AMI: *Amazon Linux 2 AMI (HVM), SSD Volume Type*

* Type: *t2-micro*

* Security Group: *my-security-group*
:
* Key Pair: *my-key-pair*

* Name: *my-ec2*

#### Supplemental Tasks

1. Terminate instance *my-ec2*

### Mount EFS Using EFS Client

1. Create an EC2 instance in default Subnet in default VPC in a Region; properties below

2. Observe Generated User Data

3. Observe resultant */etc/fstab*

Properties:

* AMI: *Amazon Linux 2 AMI (HVM), SSD Volume Type*

* Type: *t2-micro*

* Filesystem: *my-efs*

* Security Group: *my-security-group*
:
* Key Pair: *my-key-pair*

* Name: *my-ec2*

#### Supplemental Tasks

1. Terminate instance *my-ec2*

2. Delete *my-efs* EFS volume
