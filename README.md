# AWS Certified Solutions Architect – Associate

* [Domain 1: Design Resilient Architectures](1)

* [Domain 2: Design High-Performing Architectures](2)

* [Domain 3: Design Secure Applications and Architectures](3)

* [Domain 4: Design Cost-Optimized Architectures](4)

* AWS Well-Architected (CORPS)

Cost Optimization
Operational Excellence
Reliability
Performance Efficiency
Security

* Teams

Application
Infrastructure
Tools

* AWS Support Plans; greater of base or % of spend

Basic
Developer: Day, Single Contact
Business: Hours, Unlimited Contact
Enterprise: Minutes

* Use Tags to organize resources; billing or automation

**note:** A Cloud Guru; tags are case sensitive, e.g., Name vs. name

* You can use resource groups to organize your AWS resources. Resource groups make it easier to manage and automate tasks on large numbers of resources at one time.

**note:** Resource Groups are regional. Can be used with Systems Manager among other things.

* Service Health Dashboard at status.aws.amazon.com

* Personal Health Dashboard linked off Service Heatlh Dashboard (Global)

* Elasticity: Temporary scaling, Scaleablity: Permanent scaling

* Highly Available: Allow degradation, Fault Tolerant: No degradation

* Create Billing Alarm: In CloudWatch; Alarms > Billing

**note:** A Cloud Guru.  Each service has service limits that can be upped by contacting AWS. Trusted Advisor is good for telling you where problem with service limits.

### Misc

Cloud Adoption Framework

* Business

* People

* Governance

* Platform

* Security

* Operations

## Migration Strategies

* Re-Host: aka "Lift and Shift", e.g., clone to EC2

* Re-Platform: aka "Lift and Reshape", e.g., move to managed RDS

* Re-Purchase: e.g., move to Salesforce

* Re-Architecture: most comprehensive

* Retire

* Do Nothing

TOGAF: The Open Group Architectural Framework

AWS Application Discovery Service helps you plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers. Application Discovery Service is integrated with AWS Migration Hub, which simplifies your migration tracking as it aggregates your migration status information into a single console. You can view the discovered servers, group them into applications, and then track the migration status of each application from the Migration Hub console in your home region.

Cloud Transformation Maturity Model (CTMM)

* Project

* Foundation

* Migration

* Optimization

Scale Out / In: Horz., Scale Up / Down: Vert.

Naming AWS Resources:

[0-9], [a-z], [A-Z], -, ., =, +, ,, _, @

not: # or ? (hash or query)

Billing metric data is stored in the US East (N. Virginia) Region and represents worldwide charges. This data includes the estimated charges for every service in AWS that you use, in addition to the estimated overall total of your AWS charges.
