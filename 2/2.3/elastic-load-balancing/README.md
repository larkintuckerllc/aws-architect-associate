# Elastic Load Balancing

## Concepts

### Overview

> Elastic Load Balancing supports three types of load balancers: Application Load Balancers, Network Load Balancers, and Classic Load Balancers.

&nbsp;

> An Application Load Balancer functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model. After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action.

-AWS-[What Is an Application Load Balancer?](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)

> A Network Load Balancer functions at the fourth layer of the Open Systems Interconnection (OSI) model. It can handle millions of requests per second. After the load balancer receives a connection request, it selects a target from the target group for the default rule. It attempts to open a TCP connection to the selected target on the port specified in the listener configuration.

-AWS-[What Is a Network Load Balancer?](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)

> Using a Classic Load Balancer instead of an Application Load Balancer has the following benefits:

&nbsp;

> Support for EC2-Classic

&nbsp;

> Support for TCP and SSL listeners

&nbsp;

> Support for sticky sessions using application-generated cookies

-AWS-[What Is a Classic Load Balancer?](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html)

### Application Load Balancer

> A load balancer serves as the single point of contact for clients. The load balancer distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones. This increases the availability of your application. You add one or more listeners to your load balancer.

&nbsp;

> A listener checks for connection requests from clients, using the protocol and port that you configure. The rules that you define for a listener determine how the load balancer routes requests to its registered targets. Each rule consists of a priority, one or more actions, and one or more conditions. When the conditions for a rule are met, then its actions are performed. You must define a default rule for each listener, and you can optionally define additional rules.

&nbsp;

> Each target group routes requests to one or more registered targets, such as EC2 instances, using the protocol and port number that you specify. You can register a target with multiple target groups. You can configure health checks on a per target group basis. Health checks are performed on all targets registered to a target group that is specified in a listener rule for your load balancer.

![Application Load Balancer](component_architecture.png)

-AWS-[What Is an Application Load Balancer?](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)

## Exercises

### Create Target Group

#### Assumptions

Understand material in [EC2 Auto Scaling](../../2.1/ec2-auto-scaling) and completed exercises:

* Create Launch Template [EC2 Auto Scaling](../../2.1/ec2-auto-scaling)

* Create Auto Scaling Group [EC2 Auto Scaling](../../2.1/ec2-auto-scaling)

Except here install / enable *httpd* package / service instead of *stress* and manually set Auto Scaling ground with desired / minimum / maximum capacities at 3 / 3 / 3.

**note**: Also you need to create some HTML content in the file */var/www/http/index.html*.

**note**: Make sure the *my-security-group* Security Group allows HTTP inbound

#### Steps

1. Create Target Group; properties below

Properties

* Target Type: Instances

* Name: *my-target-group*

* Register Targets: Existing EC2 instances from *my-as-group*

### Create Application Load Balancer

1. Create Application Load Balancer; properties below

Properties

* Type: Application Load Balancer

* Name: *my-alb*

* Availability Zones: Same as for Auto Scaling Group

* Security Group: *my-security-group*

* Target Group: *my-target-group*

#### Supplemental Tasks

1. Validate can browse to Application Load Balancer DNS name

2. Edit *my-as-group* Auto Scaling Group; set its Target Group to *my-target-group*

3. Delete *my-alb* Application Load Balancer

4. Delete *my-target-group* Target Group

5. Delete *my-as-group* Auto Scaling Group

6. Delete *my-launch-template* Launch Template

7. Delete *my-ami* AMI

8. Delete Snapshot backing *my-ami*
