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

A launch template is similar to a launch configuration, in that it specifies instance configuration information. Included are the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and the other parameters that you use to launch EC2 instances. However, defining a launch template instead of a launch configuration allows you to have multiple versions of a template.

A launch configuration is an instance configuration template that an Auto Scaling group uses to launch EC2 instances. When you create a launch configuration, you specify information for the instances. Include the ID of the Amazon Machine Image (AMI), the instance type, a key pair, one or more security groups, and a block device mapping. If you've launched an EC2 instance before, you specified the same information in order to launch the instance.

An Auto Scaling group is associated with one launch configuration at a time, and you can't modify a launch configuration after you've created it. To change the launch configuration for an Auto Scaling group, use an existing launch configuration as the basis for a new launch configuration. Then, update the Auto Scaling group to use the new launch configuration.

If you plan to continue to use launch configurations with Amazon EC2 Auto Scaling, be aware that not all Auto Scaling group features are available. For example, you cannot create an Auto Scaling group that launches both Spot and On-Demand Instances or that specifies multiple instance types. You must use a launch template to configure these features.

When a configuration change requires replacing instances, and you have a large number of instances in your Auto Scaling group, it can be difficult to manually replace instances a few at a time. With an instance refresh, it's easier to update the instances in your Auto Scaling group.

During an instance refresh, Amazon EC2 Auto Scaling takes a set of instances out of service, terminates them, and then launches a set of instances with the new configuration. After that, instances are replaced on a rolling basis. In a rolling update, when a new instance launches, Amazon EC2 Auto Scaling waits until the instance passes a health check and completes warm-up, before moving on to replace another instance. This process repeats until all instances are replaced.

### Step / Simple Scaling

> With step scaling and simple scaling, you choose scaling metrics and threshold values for the CloudWatch alarms that trigger the scaling process. You also define how your Auto Scaling group should be scaled when a threshold is in breach for a specified number of evaluation periods.

&nbsp;

> We strongly recommend that you use a target tracking scaling policy to scale on a metric like average CPU utilization or the RequestCountPerTarget metric from the Application Load Balancer. Metrics that decrease when capacity increases and increase when capacity decreases can be used to proportionally scale out or in the number of instances using target tracking.

&nbsp;

> The main difference between the policy types is the step adjustments that you get with step scaling policies. When step adjustments are applied, and they increase or decrease the current capacity of your Auto Scaling group, the adjustments vary based on the size of the alarm breach.

&nbsp;

> In most cases, step scaling policies are a better choice than simple scaling policies, even if you have only a single scaling adjustment.

`

**note:** A Cloud Guru; Options

* Maintain level

* Scale Manually

* Scale on Schedule

* Scale on Demand

* Predictive Scaling (new)

**note:** A Cloud Guru; Cooldown prevents repeated scaling events for dynamic; default 300 seconds

### Misc

After certain actions occur, your Auto Scaling group can become unbalanced between Availability Zones. Amazon EC2 Auto Scaling compensates by rebalancing the Availability Zones.

You can attach a running EC2 instance that meets certain criteria to your Auto Scaling group. After the instance is attached, it is managed as part of the Auto Scaling group.

### Lifecycle Hooks

Lifecycle hooks enable you to perform custom actions by pausing instances as an Auto Scaling group launches or terminates them. When an instance is paused, it remains in a wait state either until you complete the lifecycle action using the complete-lifecycle-action command or the CompleteLifecycleAction operation, or until the timeout period ends (one hour by default).

You can perform a custom action using one or more of the following options:

Define an EventBridge target to invoke a Lambda function when a lifecycle action occurs. The Lambda function is invoked when Amazon EC2 Auto Scaling submits an event for a lifecycle action to EventBridge. The event contains information about the instance that is launching or terminating, and a token that you can use to control the lifecycle action. (SAME AS BELOW)

Define a notification target for the lifecycle hook. Amazon EC2 Auto Scaling sends a message to the notification target. The message contains information about the instance that is launching or terminating, and a token that you can use to control the lifecycle action.

Create a script that runs on the instance as the instance starts. The script can control the lifecycle action using the ID of the instance on which it runs.

### Maximum Instance Lifetime

When you use the AWS Management Console to update an Auto Scaling group, or when you use the AWS CLI or AWS SDKs to create or update an Auto Scaling group, you can set the optional maximum instance lifetime parameter. The maximum instance lifetime feature does the work of replacing instances that have been in service for the maximum amount of time allowed.

When configuring the maximum instance lifetime for your Auto Scaling group, you must specify a value of at least 604,800 seconds (7 days). To clear a previously set value, specify a new value of 0.

Depending on the maximum duration specified and the size of the Auto Scaling group, the rate of replacement may vary. In general, Amazon EC2 Auto Scaling replaces instances one at a time, with a pause in between replacements. However, the rate of replacement will be higher when there is not enough time to replace each instance individually based on the maximum duration that you specified. In this case, Amazon EC2 Auto Scaling will replace several instances at once, by up to 10 percent of the current capacity of your Auto Scaling group at a time.

### Instance Refresh

During an instance refresh, Amazon EC2 Auto Scaling takes a set of instances out of service, terminates them, and then launches a set of instances with the new configuration. After that, instances are replaced on a rolling basis. In a rolling update, when a new instance launches, Amazon EC2 Auto Scaling waits until the instance passes a health check and completes warm-up, before moving on to replace another instance. This process repeats until all instances are replaced.

Before starting an instance refresh, you can configure the minimum healthy percentage to control the level of disruption to your application. If your application doesn't pass health checks, the rolling update process waits for a time period of up to 60 minutes after it reaches the minimum healthy threshold before it eventually fails. The intention is to give it time to recover in case of a temporary issue. If the rolling update process fails, any instances that were already replaced are not rolled back to their previous configuration. To fix a failed instance refresh, first resolve the underlying issue that caused the update to fail, and then initiate another instance refresh.

After determining that a newly launched instance is healthy, Amazon EC2 Auto Scaling does not immediately move on to the next replacement. It provides a window for each instance to warm up after launching, which you can configure.

### ELB

The default health checks for an Auto Scaling group are EC2 status checks only. If an instance fails these status checks, the Auto Scaling group considers the instance unhealthy and replaces it.

If you configure the Auto Scaling group to use ELB health checks, it considers the instance unhealthy if it fails either the EC2 status checks or the ELB health checks. If you attach multiple load balancer target groups or Classic Load Balancers to the group, all of them must report that the instance is healthy in order for it to consider the instance healthy. If any one of them reports an instance as unhealthy, the Auto Scaling group replaces the instance, even if other ones report it as healthy.

## Exercises

### Create Launch Template

#### Assumptions

Understand material in [Elastic Cloud Compute (EC2)](../ec2) and completed exercises:

* Create Key Pair [Elastic Cloud Compute (EC2)](../ec2)

* Create Security Group [Elastic Cloud Compute (EC2)](../ec2)

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

4. Observe that deleting Auto Scaling Groups delete their associate EC2 Instances

5. Delete *my-launch-template* Launch Template

6. Deregister *my-ami* AMI

7. Delete Snapshot backing the *my-ami* AMI
