# Amazon Virtual Private Cloud (VPC)

## Concepts

### Overview

> Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

-AWS-[What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)

### Default VPC

![Default VPC](default.png)

### Public / Private VPC

![Private VPC](private.png)

### Misc

> VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data can be published to Amazon CloudWatch Logs or Amazon S3.

-AWS-[VPC Flow logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html)

![Direct Connect](direct_connect_overview.png)

-AWS-[What is AWS Direct Connect?](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)

> A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.

&nbsp;

> Endpoints are virtual devices. They are horizontally scaled, redundant, and highly available VPC components. They allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.

&nbsp;

> There are two types of VPC endpoints: interface endpoints and gateway endpoints. Create the type of VPC endpoint required by the supported service.

-AWS-[VPC endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html)

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
