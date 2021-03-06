# 3.3 Select appropriate data security options

* [AWS Key Management Service (KMS)](kms)

* AWS Systems Manager: AWS Systems Manager is an AWS service that you can use to view and control your infrastructure on AWS.

Quick Setup is a tool you can use to quickly configure required security roles and commonly used Systems Manager capabilities on your EC2 instances.

Explorer is a customizable operations dashboard that reports information about your AWS resources.

OpsCenter provides a central location where operations engineers and IT professionals can view, investigate, and resolve operational work items (OpsItems) related to AWS resources.

Amazon CloudWatch Dashboards are customizable home pages in the CloudWatch console that you can use to monitor your resources in a single view, even those resources that are spread across different regions.

With Resource Groups, you can create a custom console that organizes and consolidates information based on criteria that you specify in tags. You can also use groups as the basis for viewing monitoring and configuration insights in AWS Systems Manager.

AppConfig helps you create, manage, and quickly deploy application configurations. AppConfig supports controlled deployments to applications of any size.

*Parameter Store provides secure, hierarchical storage for configuration data and secrets management.*

**note:** A Cloud Guru; versioned (rollback); TTL; up to 15 levels deep; access can be granted using hiearchical; can reference in CloudFormation. No cost. Up to 10K.

Use Systems Manager Automation to automate common maintenance and deployment tasks.

Change Calendar lets you set up date and time ranges when actions you specify (for example, in Systems Manager Automation documents) may or may not be performed in your AWS account.

*Use Maintenance Windows to set up recurring schedules for managed instances to run administrative tasks like installing patches and updates without interrupting business-critical operations.*

Use Systems Manager Configuration Compliance to scan your fleet of managed instances for patch compliance and configuration inconsistencies.

Inventory Manager automates the process of collecting software inventory from managed instances.

A managed instance is any EC2 instance or on-premises machine–a server or a virtual machine (VM)–in your hybrid environment that is configured for Systems Manager.

To set up servers and VMs in your hybrid environment as managed instances, you need to create a managed-instance activation.

*Use Session Manager to manage your EC2 instances through an interactive one-click browser-based shell or through the AWS CLI.*

*Use Systems Manager Run Command to remotely and securely manage the configuration of your managed instances at scale.*

Use Systems Manager State Manager to automate the process of keeping your managed instances in a defined state.

*Use Patch Manager to automate the process of patching your managed instances with both security related and other types of updates.*

Use Distributor to create and deploy packages to managed instances.

* AWS Service Catalog: AWS Service Catalog enables organizations to create and manage catalogs of IT services that are approved for use on AWS. These IT services can include everything from virtual machine images, servers, software, and databases to complete multi-tier application architectures. AWS Service Catalog allows organizations to centrally manage commonly deployed IT services, and helps organizations achieve consistent governance and meet compliance requirements. End users can quickly deploy only the approved IT services they need, following the constraints set by your organization.

> You create a product by importing an AWS CloudFormation template. AWS CloudFormation templates define the AWS resources required for the product, the relationships between resources, and the parameters that end users can plug in when they launch the product to configure security groups, create key pairs, and perform other customizations.

&nbsp;

> Granting a user access to a portfolio enables that user to browse the portfolio and launch the products in it.

&nbsp;

> When a user launches a product that has an IAM role assigned to it, AWS Service Catalog uses the role to launch the product's cloud resources using AWS CloudFormation.

&nbsp;

> You also can share your portfolios with other AWS accounts and allow the administrator of those accounts to distribute your portfolios with additional constraints, such as limiting which EC2 instances a user can create. Through the use of portfolios, permissions, sharing, and constraints, you can ensure that users are launching products that are configured properly for the organization’s needs and standards.

**note:** Launch Constraint = Role to Launch, Notification Constraint = SNS Topic on Stack details, Template Contraint = Wizard to limit features. When another account uses a portfolio, they need to supply their own Role to Launch.

* Amazon CloudWatch: Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.

* AWS Inspector: Amazon Inspector tests the network accessibility of your Amazon EC2 instances and the security state of your applications that run on those instances. Amazon Inspector assesses applications for exposure, vulnerabilities, and deviations from best practices. After performing an assessment, Amazon Inspector produces a detailed list of security findings that is organized by level of severity.

**note:** A Cloud Guru; uses tags to target. Requires its own agent. Multiple rules package.

> AWS CloudHSM provides hardware security modules in the AWS Cloud. A hardware security module (HSM) is a computing device that processes cryptographic operations and provides secure storage for cryptographic keys.

**note:**: A Cloud Guru. FIPS 140-3; single tenant multi-az (you have to enable). You supply the key and it runs in a VPC. No AWS API; you use third-party solution. It runs in its own VPC and exposes ENI (like PrivateLink) into your VPC.

**note:** Classic CloudHSM is expensive upfront and not redundant; new CloudHSM has no upfront cost and is redundant.

> Secrets Manager enables you to replace hardcoded credentials in your code, including passwords, with an API call to Secrets Manager to retrieve the secret programmatically. This helps ensure the secret can't be compromised by someone examining your code, because the secret no longer exists in the code. Also, you can configure Secrets Manager to automatically rotate the secret for you according to a specified schedule. This enables you to replace long-term secrets with short-term ones, significantly reducing the risk of compromise.

**note:** A Cloud Guru. Cost. Full secrets rotation integration with RDS. Can use Lambda trigger on a key rotation. Can generate random secrets. Can be shared across accounts.

**note:** A Cloud Guru. Amplification Attach (legit servers tricked into sending to spoofed IP), Slowloris Attack (sends partial requests to keep open connections)

> AWS provides AWS Shield Standard and AWS Shield Advanced for protection against DDoS attacks. AWS Shield Standard is automatically included at no extra cost beyond what you already pay for AWS WAF and your other AWS services. For added protection against DDoS attacks, AWS offers AWS Shield Advanced. AWS Shield Advanced provides expanded DDoS attack protection for your Amazon Elastic Compute Cloud instances, Elastic Load Balancing load balancers, Amazon CloudFront distributions, Amazon Route 53 hosted zones, and your AWS Global Accelerator accelerators.

**note:** Advanced is $3,000 / month  / org. Gain access to DDoS Response Team (DRT)

> AWS WAF is a web application firewall that lets you monitor the HTTP(S) requests that are forwarded to an Amazon CloudFront distribution, an Amazon API Gateway REST API, or an Application Load Balancer.

AWS WAF also lets you control access to your content. Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, an Amazon CloudFront distribution, an Amazon API Gateway REST API, or an Application Load Balancer responds to requests either with the requested content or with an HTTP 403 status code (Forbidden). You can also configure CloudFront to return a custom error page when a request is blocked.

**note:** A Cloud Guru; Uses filtering rules, e.g., ip addresses, sql injection, etc. Returns 403 code if fails. Allow except, Allow only, or count.

> AWS Firewall Manager simplifies your AWS WAF, AWS Shield Advanced, and Amazon VPC security groups administration and maintenance tasks across multiple accounts and resources. With Firewall Manager, you set up your AWS WAF firewall rules, Shield Advanced protections, and Amazon VPC security groups just once. The service automatically applies the rules and protections across your accounts and resources, even as you add new resources.

* AWS Trusted Advisor is an online resource to help you reduce cost, increase performance, and improve security by optimizing your AWS environment. AWS Trusted Advisor provides real-time guidance to help you provision your resources following AWS best practices.

**note:** A Cloud Guru; requires at least business or enterprise support plans.

## DDOS

UDP reflection attacks exploit the fact that UDP is a stateless protocol. Attackers can
craft a valid UDP request packet listing the attack target’s IP as the UDP source IP
address. The attacker has now falsified—spoofed—the UDP request packet’s source
IP. An attacker then sends the UDP packet containing the spoofed source IP to an
intermediate server. The server is tricked into sending its UDP response packets to the
targeted victim IP rather than back to the attacker’s IP address. 

In a SYN flood attack, a malicious client sends a large number of SYN packets, but
never sends the final ACK packets to complete the handshakes. The server is left
waiting for a response to the half-open TCP connections and eventually runs out of
capacity to accept new TCP connections. 

In an HTTP flood attack, an attacker sends HTTP requests that appear to be from a
real user of the web application. Some HTTP floods target a specific resource, while
more complex HTTP floods attempt to emulate human interaction with the application.

Cache-busting attacks are a type of HTTP flood that uses variations in the query string
to circumvent content delivery network (CDN) caching.

With a WordPress XML-RPC flood attack, also known as a WordPress pingback
flood, an attacker misuses the XML-RPC API function of a website hosted on the
WordPress content management software to generate a flood of HTTP requests.

Application layer attacks can also target domain name system (DNS) services. The
most common of these attacks is a DNS query flood in which an attacker uses many
well-formed DNS queries to exhaust the resources of a DNS server.

If a web application is delivered over TLS, an attacker can also choose to attack the
TLS negotiation process. TLS is computationally expensive so an attacker can reduce a
server’s availability by sending unintelligible data.
