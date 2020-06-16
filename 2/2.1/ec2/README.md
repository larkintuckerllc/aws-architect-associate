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

nbsp;

> Instances that are in any other state aren't billed.

-AWS-[How are EC2 instance-hours billed?](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-instance-hour-billing/)

### Custom AMI

> First, launch an instance from an AMI that's similar to the AMI that you'd like to create. You can connect to your instance and customize it. When the instance is configured correctly, ensure data integrity by stopping the instance before you create an AMI, then create the image. 

&nbsp;

> During the AMI-creation process, Amazon EC2 creates snapshots of your instance's root volume and any other EBS volumes attached to your instance. You're charged for the snapshots until you deregister the AMI and delete the snapshots.

&nbsp;

> If you have a snapshot of the root device volume of an instance, you can create an AMI from this snapshot using the AWS Management Console or the command line.

-AWS-[Creating an Amazon EBS-backed Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html)

## Challenges

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

1. Observe EBS volume is marked by default *Delete on termination*

2. Update instance packages

3. Stop instance

### Create EC2 Spot Instance

* Same as Create EC2 Instance except Name: *my-spot-ec2*

**note**: Tried multiple regions; repeatedly got error trying to launch

#### Supplemental Tasks

1. Observe price difference between On-Demand and Spot pricing

2. Teminate instance

### Create Custom AMI

* Regional resource

* From *my-ec2* instance

* Name: *my-ami*

#### Supplemental Tasks

1. Create and terminate EC2 instance using *my-ami* AMI

2. Delete AMI

### User Data

TODO
