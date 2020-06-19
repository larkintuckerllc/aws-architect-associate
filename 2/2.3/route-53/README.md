# Amazon Route 53

## Concepts

### Overview

> Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service. You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking.

-AWS-[What is Amazon Route 53?](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)

It is important to know the various DNS record types; described in [Amazon Route 53 concepts](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/route-53-concepts.html).

> When you create a record, you choose a routing policy, which determines how Amazon Route 53 responds to queries:

&nbsp;

> Simple routing policy – Use for a single resource that performs a given function for your domain, for example, a web server that serves content for the example.com website.

&nbsp;

> Failover routing policy – Use when you want to configure active-passive failover.

&nbsp;

> Geolocation routing policy – Use when you want to route traffic based on the location of your users.

&nbsp;

> Geoproximity routing policy – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.

&nbsp;

> Latency routing policy – Use when you have resources in multiple AWS Regions and you want to route traffic to the region that provides the best latency.

&nbsp;

> Multivalue answer routing policy – Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random.

&nbsp;

> Weighted routing policy – Use to route traffic to multiple resources in proportions that you specify.

-AWS-[Choosing a routing policy](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)

> Amazon Route 53 alias records provide a Route 53–specific extension to DNS functionality. Alias records let you route traffic to selected AWS resources, such as CloudFront distributions and Amazon S3 buckets.

&nbsp;

> When you use an alias record to route traffic to an AWS resource, Route 53 automatically recognizes changes in the resource. For example, suppose an alias record for example.com points to an ELB load balancer at lb1-1234.us-east-2.elb.amazonaws.com. If the IP address of the load balancer changes, Route 53 automatically starts to respond to DNS queries using the new IP address.

-AWS-[Choosing between alias and non-alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html)

### Sidebar into Certificate Manager

> AWS Certificate Manager (ACM) handles the complexity of creating, storing, and renewing public SSL/TLS X.509 certificates and keys that protect your AWS websites and applications. You can provide certificates for supported AWS services either by issuing them directly with ACM or by importing third-party certificates into the ACM management system. 

-AWS-[What Is AWS Certificate Manager?](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)

## Exercises

### Register a Domain Name

1. Register a domain name

### Create *A* Record to IP Address

#### Assumptions

Understand material in [Elastic Cloud Compute (EC2)](../../2.1/ec2) and completed exercises:

* Create Key Pair [Elastic Cloud Compute (EC2)](../../2.1/ec2)

* Create Security Group [Elastic Cloud Compute (EC2)](../../2.1/ec2)

**note**: Make sure Security Group enables inbound HTTP

#### Tasks

1. Create an EC2 instance in default Subnet in default VPC in a Region; properties below

2. Login and update instance packages

3. Install, enable, and start *httpd*; create HTML file */var/www/http/index.html*

4. Allocate and assign Elastic IP address to *my-ec2* EC2 Instance

5. Create *A* record to Elastic IP address; e.g., *www.todosrus.com*

EC2 Instance Properties

* AMI: *Amazon Linux 2 AMI (HVM), SSD Volume Type*

* Type: *t2-micro*

* Security Group: *my-security-group*
:
* Key Pair: *my-key-pair*

* Name: *my-ec2*

### Create Alias *A* Record to *A* Record

1. Create Alias *A* record, e.g., *todosrus.com*, for root to *A* record, e.g., *www.todosrus.com*

2. Observe web addresses in browser

#### Supplemental Tasks

1. Delete Alias *A* record

2. Delete *A* record

3. Dissassociate and release Elastic IP address

4. Terminate *my-ec2* EC2 Instance

### Create Alias *A* Record to Elastic Load Balancer

#### Assumptions

Understand material in [Elastic Load Balancing](../load-balancing) and completed exercises:

* [Create Application Load Balancer](../load-balancing)

#### Tasks

1. Create Alias *A* record to Elastic Load Balancer, e.g., *www.todosrus.com*

### Add HTTPS Listener to Application Load Balancer

1. Create wildcard certificate for domain, e.g., **.todosrus.com* and *todosrus.com*

2. Add new HTTPS listener routing to *my-target-group* for *my-alb* using certificate

3. Add HTTPS to *my-security-group* Security Group

4. Validate can browse to HTTPS endpoint

5. Replace HTTP listener to redirect to HTTPS on *my-alb*

6. Create Alias *A* apex record, e.g., *todosrus.com*, to *A* record, e.g., *www.todosrus.com*

7. Add a rule to the HTTPS listener to redirect traffic to apex record to redirect to *A* record, e.g., *www.todosrus.com*.

#### Supplemental Tasks

1. Delete Alias *A* records

2. Delete objects as per *Supplemental Tasks* in exercise [Create Application Load Balancer](../load-balancing)
