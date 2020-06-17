# Elastic Cloud Computer (EC2)

## Concepts

### Overview

> Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) cloud. Using Amazon EC2 eliminates your need to invest in hardware up front, so you can develop and deploy applications faster. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage. Amazon EC2 enables you to scale up or down to handle changes in requirements or spikes in popularity, reducing your need to forecast traffic.

-AWS-[What is Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)

### Key Pair

> AWS uses public-key cryptography to secure the login information for your instance. A Linux instance has no password; you use a key pair to log in to your instance securely. You specify the name of the key pair when you launch your instance, then provide the private key when you log in using SSH.

-AWS-[Setting up with Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html)

### Security Group

> Security groups act as a firewall for associated instances, controlling both inbound and outbound traffic at the instance level. You must add rules to a security group that enable you to connect to your instance from your IP address using SSH. You can also add rules that allow inbound and outbound HTTP and HTTPS access from anywhere.

-AWS-[Setting up with Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html)

![EC2](ec2.png)

-AWS-[Getting started with Amazon EC2 Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)

### Pricing

> On-Demand: With On-Demand instances, you pay for compute capacity by the hour or the second depending on which instances you run.

&nbsp;

> Spot-Instance: Amazon EC2 Spot instances allow you to request spare Amazon EC2 computing capacity for up to 90% off the On-Demand price

&nbsp;

> Savings Plans: Savings Plans are a flexible pricing model that offer low prices on EC2 and Fargate usage, in exchange for a commitment to a consistent amount of usage (measured in $/hour) for a 1 or 3 year term.

&nbsp;

> Reserved Instances: Reserved Instances provide you with a significant discount (up to 75%) compared to On-Demand instance pricing. In addition, when Reserved Instances are assigned to a specific Availability Zone, they provide a capacity reservation, giving you additional confidence in your ability to launch instances when you need them.

&nbsp;

> Dedicated Host: A Dedicated Host is a physical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses, including Windows Server, SQL Server, and SUSE Linux Enterprise Server (subject to your license terms), and can also help you meet compliance requirements

-AWS-[Amazon EC2 Pricing](https://aws.amazon.com/ec2/pricing/)

> EC2 usage is calculated by either the hour or the second, depending on which AMI you're running.

&nbsp;

> When reviewing your EC2 usage, consider the following:

&nbsp;

> If your instance is billed by the hour, then you're billed for a minimum of one hour each time a new instance is started—that is, when it enters the running state.

&nbsp;

> If your instance is billed by the second, then you're billed for a minimum of 60 seconds each time a new instance is started—that is, when it enters the running state.

&nbsp;

> Instances that are in any other state aren't billed.

-AWS-[How are EC2 instance-hours billed?](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-instance-hour-billing/)

### AMI Properties

> Linux Amazon Machine Images use one of two types of virtualization: paravirtual (PV) or hardware virtual machine (HVM). The main differences between PV and HVM AMIs are the way in which they boot and whether they can take advantage of special hardware extensions (CPU, network, and storage) for better performance.

&nbsp;

> For the best performance, we recommend that you use current generation instance types and HVM AMIs when you launch your instances.

-AWS-[Linux AMI virtualization types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html)

> When you launch an instance, the root device volume contains the image used to boot the instance. When we introduced Amazon EC2, all AMIs were backed by Amazon EC2 instance store, which means the root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3. After we introduced Amazon EBS, we introduced AMIs that are backed by Amazon EBS. This means that the root device for an instance launched from the AMI is an Amazon EBS volume created from an Amazon EBS snapshot.

&nbsp;

> You can choose between AMIs backed by Amazon EC2 instance store and AMIs backed by Amazon EBS. We recommend that you use AMIs backed by Amazon EBS, because they launch faster and use persistent storage.

-AWS-[Amazon EC2 root device volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/RootDeviceStorage.html)

### Monitoring

> System status checks – monitor the AWS systems required to use your instance to ensure that they are working properly. These checks detect problems with your instance that require AWS involvement to repair.

&nbsp;

> Instance status checks – monitor the software and network configuration of your individual instance. These checks detect problems that require your involvement to repair.

&nbsp;

> Amazon CloudWatch alarms – watch a single metric over a time period you specify, and perform one or more actions based on the value of the metric relative to a given threshold over a number of time periods.

-AWS-[Automated and manual monitoring](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring_automated_manual.html)

> By default, Amazon EC2 sends metric data to CloudWatch in 5-minute periods. To send metric data for your instance to CloudWatch in 1-minute periods, you can enable detailed monitoring on the instance.

-AWS-[Monitoring your instances using CloudWatch](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-cloudwatch.html)

**note:** Collecting more system-level metrics, e.g., memory and disk utilization, and logs requires installing and configuring the CloudWatch Agent.

### Tagging

> A tag is a label that you assign to an AWS resource. Each tag consists of a key and an optional value, both of which you define.

&nbsp;

Tags enable you to categorize your AWS resources in different ways, for example, by purpose, owner, or environment. This is useful when you have many resources of the same type—you can quickly identify a specific resource based on the tags you've assigned to it. For example, you could define a set of tags for your account's Amazon EC2 instances that helps you track each instance's owner and stack level.

-AWS-[Tagging your Amazon EC2 resources](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html)

### Elastic IP

> An Elastic IP address is a static IPv4 address designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account. With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.

-AWS-[Elastic IP addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

### Custom AMI

> First, launch an instance from an AMI that's similar to the AMI that you'd like to create. You can connect to your instance and customize it. When the instance is configured correctly, ensure data integrity by stopping the instance before you create an AMI, then create the image. 

&nbsp;

> During the AMI-creation process, Amazon EC2 creates snapshots of your instance's root volume and any other EBS volumes attached to your instance. You're charged for the snapshots until you deregister the AMI and delete the snapshots.

&nbsp;

> If you have a snapshot of the root device volume of an instance, you can create an AMI from this snapshot using the AWS Management Console or the command line.

-AWS-[Creating an Amazon EBS-backed Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html)

## Exercises

### Create Key Pair

* Regional resource

* Name: *my-key-pair*

### Create Security Group

* Related to Regional Resource VPC

* Enable Inbound SSH from 0.0.0.0/0

* Name: *my-security-group*

### Create EC2 Instance

* Related to Subnet Related to Regional Resource VPC

* AMI: Amazon Linux 2 AMI (HVM), SSD Volume Type

* Type: t2-micro

* Security Group: my-security-group

* Key Pair: my-key-pair

* Name: *my-ec2*

#### Supplemental Tasks

1. Observe AMI virtualization type (HVM)

2. Observe root volume is EBS (not Instance Store)

3. Observe EBS volume is marked by default *Delete on termination*

4. Update instance packages

5. Stop instance

### Create EC2 Spot Instance

* Same as Create EC2 Instance except Name: *my-spot-ec2*

**note**: Tried multiple regions; repeatedly got error trying to launch.

#### Supplemental Tasks

1. Observe price difference between On-Demand and Spot pricing

2. Teminate instance

### Monitor EC2 Instance

1. Start *my-ec2* instance

2. Observe System and Instance Status Checks

3. Create Alarm *my-alarm* to *my-topic* Topic if CPU average is at 50% for 5 minute

4. Install *stress* CLI tool; requires enabling EPEL repo in Linux 2 AMI

5. Using *stress* CLI, stress CPU for 5 minutes; observe alarm

#### Supplemental Tasks

1. Observe no memory or disk utilization metrics

2. Stop *my-ec2* instance

### Add Tag to *my-ec2* Instance

* Tag: my-tag

* Value: my-value

### Associate Elastic IP Address

1. Allocate Elastic IP Address

2. Associate Elastic IP Address to *my-ec2* instance

#### Supplemental Tasks

1. Disassociate Elastic IP Address from *my-ec2* instance

2. Deallocate Elastic IP Address

### Meta ? User Data

TODO

### Change Instance Type

TODO

### Create Custom AMI

* Regional resource

* From *my-ec2* instance

* Name: *my-ami*

#### Supplemental Tasks

1. Create and terminate EC2 instance using *my-ami* AMI

### Copy an AMI

TODO

### Service Quota

TODO