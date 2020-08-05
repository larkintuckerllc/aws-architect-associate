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

* Amazon CloudWatch: Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.

* AWS Inspector: Amazon Inspector tests the network accessibility of your Amazon EC2 instances and the security state of your applications that run on those instances. Amazon Inspector assesses applications for exposure, vulnerabilities, and deviations from best practices. After performing an assessment, Amazon Inspector produces a detailed list of security findings that is organized by level of severity.
