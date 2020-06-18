# EC2 Auto Scaling

## Concepts

### Overview

> Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application. You create collections of EC2 instances, called Auto Scaling groups. You can specify the minimum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size. You can specify the maximum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size. If you specify the desired capacity, either when you create the group or at any time thereafter, Amazon EC2 Auto Scaling ensures that your group has this many instances. If you specify scaling policies, then Amazon EC2 Auto Scaling can launch or terminate instances as demand on your application increases or decreases.

![EC2 Auto Scaling](as-basic-diagram.png)

> Your EC2 instances are organized into groups so that they can be treated as a logical unit for the purposes of scaling and management. When you create a group, you can specify its minimum, maximum, and, desired number of EC2 instances.

&nbsp;

> Your group uses a launch template or a launch configuration as a configuration template for its EC2 instances. You can specify information such as the AMI ID, instance type, key pair, security groups, and block device mapping for your instances

&nbsp;

> Amazon EC2 Auto Scaling provides several ways for you to scale your Auto Scaling groups. For example, you can configure a group to scale based on the occurrence of specified conditions (dynamic scaling) or on a schedule. 

-AWS-[What Is Amazon EC2 Auto Scaling?](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)

> We recommend that you create Auto Scaling groups from launch templates to ensure that you're getting the latest features from Amazon EC2.

-AWS-[Launch Templates](https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchTemplates.html)

### Step / Simple Scaling

> With step scaling and simple scaling, you choose scaling metrics and threshold values for the CloudWatch alarms that trigger the scaling process. You also define how your Auto Scaling group should be scaled when a threshold is in breach for a specified number of evaluation periods.

&nbsp;

> We strongly recommend that you use a target tracking scaling policy to scale on a metric like average CPU utilization or the RequestCountPerTarget metric from the Application Load Balancer. Metrics that decrease when capacity increases and increase when capacity decreases can be used to proportionally scale out or in the number of instances using target tracking.

&nbsp;

> The main difference between the policy types is the step adjustments that you get with step scaling policies. When step adjustments are applied, and they increase or decrease the current capacity of your Auto Scaling group, the adjustments vary based on the size of the alarm breach.

&nbsp;

> In most cases, step scaling policies are a better choice than simple scaling policies, even if you have only a single scaling adjustment.

-AWS-[Step and Simple Scaling Policies for Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/as-scaling-simple-step.html)

## Exercises

### Create Launch Template

#### Assumptions

Understand material in [ec2](../ec2) and completed exercises:

* Create Key Pair [ec2](../ec2)

* Create Security Group [ec2](../ec2)

#### Tasks

1. Create an EC2 instance in default Subnet in default VPC in a Region; properties below

2. Login and update instance packages

3. Install *stress* CLI tool; requires enabling EPEL repo in Linux 2 AMI

4. Create AMI named *my-ami* from *my-ec2* EC2 Instance in Region

5. Create Launch Template;  properties below

EC2 Instance Properties

* AMI: *Amazon Linux 2 AMI (HVM), SSD Volume Type*

* Type: *t2-micro*

* Security Group: *my-security-group*
:
* Key Pair: *my-key-pair*

* Name: *my-ec2*

Launch Template Properties

* Name: *my-launch-template*

* AMI: *my-ami*

* Instance type: *t2-micro*

* Key pair: *my-key-pair*

* Security Groups: *my-security-group*

#### Supplemental Tasks

1. Terminate *my-ec2* EC2 Instance

### Create Auto Scaling Group

* Name: *my-as-group*

* Launch Template: *my-launch-template*

* Select one or more subnets in default VPC in Region

* Desired / Minimum / Maximum Capacities: 1 / 1 / 3

* Target Tracking Scaling Policy: Average CPU 50%

#### Supplemental Tasks

1. Using *stress* CLI, stress CPU for 5 minutes; observe scaling

2. Observe that Target Tracking Scaling Polices only support the default EC2 metrics, e.g., CPU.  For example, in order to scale on memory, one will need to Step / Simple Scaling Polices

3. Delete *my-as-group* Auto Scaling Group
