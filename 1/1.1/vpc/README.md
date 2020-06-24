# Amazon Virtual Private Cloud (VPC)

## Concepts

### Overview

> Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

-AWS-[What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)

### Default VPC

![Default VPC](default.png)

### Public / Private VPC

![Private VPC](private.png)

## Exercises

### Review Elements of Default VPC

1. VPC: Region and CIDR

2. Internet Gateway

3. Subnet: AZ and CIDR

4. Route Table: Subnet and routes (Public)

5. Network Access Control List (NACL): Stateless firewall, Subnet, and IB and OB rules

6. Security Group: Stateful firewall, VPC, and IB and OB rules

### Create VPC with Public and Private Subnets

1. Create VPC with public and private

#### Supplemental Tasks

1. Tear out
