# Amazon Elastic Block Store (EBS)

## Concepts

### Overview

> Amazon Elastic Block Store (Amazon EBS) provides block level storage volumes for use with EC2 instances. EBS volumes behave like raw, unformatted block devices. You can mount these volumes as devices on your instances. EBS volumes that are attached to an instance are exposed as storage volumes that persist independently from the life of the instance. You can create a file system on top of these volumes, or use them in any way you would use a block device (such as a hard drive). You can dynamically change the configuration of a volume attached to an instance.

&nbsp;

> EBS volumes are created in a specific Availability Zone, and can then be attached to any instances in that same Availability Zone. To make a volume available outside of the Availability Zone, you can create a snapshot and restore that snapshot to a new volume anywhere in that Region. You can copy snapshots to other Regions and then restore them to new volumes there, making it easier to leverage multiple AWS Regions for geographical expansion, data center migration, and disaster recovery.

&nbsp;

> General Purpose SSD volumes offer a base performance of 3 IOPS/GiB, with the ability to burst to 3,000 IOPS for extended periods of time. These volumes are ideal for a broad range of use cases such as boot volumes, small and medium-size databases, and development and test environments.

&nbsp;

> Provisioned IOPS SSD volumes support up to 64,000 IOPS and 1,000 MiB/s of throughput. This allows you to predictably scale to tens of thousands of IOPS per EC2 instance.

&nbsp;

> Throughput Optimized HDD volumes provide low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. These volumes are ideal for large, sequential workloads such as Amazon EMR, ETL, data warehouses, and log processing.

&nbsp;

> Cold HDD volumes provide low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. These volumes are ideal for large, sequential, cold-data workloads. If you require infrequent access to your data and are looking to save costs, these volumes provides inexpensive block storage.

-AWS-[Amazon Elastic Block Store (Amazon EBS)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)

> After you attach an Amazon EBS volume to your instance, it is exposed as a block device. You can format the volume with any file system and then mount it. After you make the EBS volume available for use, you can access it in the same ways that you access any other volume. Any data written to this file system is written to the EBS volume and is transparent to applications using the device.

-AWS-[Making an Amazon EBS volume available for use on Linux](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html)

## Exercises

### Create EBS Volume

1. Create EBS volume; properties below

Properties:

* Type: gp2

* Size: 1 GB

* Name: *my-ebs*

*note*: Need to be aware which AZ place in.

### Mount EBS Volume on to an EC2 Instance

#### Assumptions

Understand material in [Elastic Cloud Compute (EC2)](../../../2/2.1/ec2) and completed exercises:

* Create Key Pair [Elastic Cloud Compute (EC2)](../../../2/2.1/ec2)

* Create Security Group [Elastic Cloud Compute (EC2)](../../../2/2.1/ec2)

**note**: Make sure Security Group enables inbound HTTP

#### Tasks

1. Create an EC2 instance in a subnet in default VPC in a Region; properties below

2. Login and update instance packages

3. Install, enable, and start *httpd*; create HTML file */var/www/http/index.html*

4. Attach *my-ebs* Volume to *my-ec2* EC2 Instance

5. Format and mount EBS volume on */var/www/html*

6. Set volume to auto-mount on boot

7. Create HTML file at */var/www/html/index.html*

8. Verify can browse to public DNS name

Properties

* AMI: *Amazon Linux 2 AMI (HVM), SSD Volume Type*

* Type: *t2-micro*

* Security Group: *my-security-group*

* Key Pair: *my-key-pair*

* Name: *my-ec2*

* Subnet: Same as where EBS volume was created
