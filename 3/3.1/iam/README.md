# AWS Identity Access Management (IAM)

## Concepts

### Overview

> AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.

&nbsp;

> When you first create an AWS account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS account root user and is accessed by signing in with the email address and password that you used to create the account. We strongly recommend that you do not use the root user for your everyday tasks, even the administrative ones. Instead, adhere to the best practice of using the root user only to create your first IAM user. Then securely lock away the root user credentials and use them to perform only a few account and service management tasks.

-AWS-[What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

> Instead of sharing your root user credentials with others, you can create individual IAM users within your account that correspond to users in your organization. IAM users are not separate accounts; they are users within your account. Each user can have its own password for access to the AWS Management Console. You can also create an individual access key for each user so that the user can make programmatic requests to work with resources in your account.

-AWS-[Overview of Identity Management: Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_identity-management.html)

> You can organize IAM users into IAM groups and attach a policy to a group. In that case, individual users still have their own credentials, but all the users in a group have the permissions that are attached to the group

&nbsp;

> You give permissions to a user by creating an identity-based policy, which is a policy that is attached to the user or a group to which the user belongs.

&nbsp;

> Actions or resources that are not explicitly allowed are denied by default.

&nbsp;

> Identity-based policies are permissions policies that you attach to an IAM identity, such as an IAM user, group, or role. Resource-based policies are permissions policies that you attach to a resource such as an Amazon S3 bucket or an IAM role trust policy.

&nbsp;

> Identity-based policies can be further categorized:

&nbsp;

> Managed policies – Standalone identity-based policies that you can attach to multiple users, groups, and roles in your AWS account. You can use two types of managed policies:

&nbsp;

> AWS managed policies – Managed policies that are created and managed by AWS. If you are new to using policies, we recommend that you start by using AWS managed policies.

&nbsp;

> Customer managed policies – Managed policies that you create and manage in your AWS account. Customer managed policies provide more precise control over your policies than AWS managed policies. You can create and edit an IAM policy in the visual editor or by creating the JSON policy document directly. For more information, see Creating IAM Policies and Editing IAM Policies.

&nbsp;

> Inline policies – Policies that you create and manage and that are embedded directly into a single user, group, or role. In most cases, we don't recommend using inline policies.

&nbsp;

> Resource-based policies control what actions a specified principal can perform on that resource and under what conditions. Resource-based policies are inline policies, and there are no managed resource-based policies.

![Policy Diagram](policy_summaries-diagram.png)

-AWS-[Overview of Access Management: Permissions and Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html)

> The evaluation logic for a request within a single account follows these rules:

&nbsp;

> By default, all requests are implicitly denied. (Alternatively, by default, the AWS account root user has full access.)

&nbsp;

> An explicit allow in an identity-based or resource-based policy overrides this default.

&nbsp;

> If a permissions boundary, Organizations SCP, or session policy is present, it might override the allow with an implicit deny.

&nbsp;

> An explicit deny in any policy overrides any allows.

-AWS-[Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html)

### Roles

> An IAM identity that you can create in your account that has specific permissions. An IAM role has some similarities to an IAM user. Roles and users are both AWS identities with permissions policies that determine what the identity can and cannot do in AWS. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it. Also, a role does not have standard long-term credentials such as a password or access keys associated with it. Instead, when you assume a role, it provides you with temporary security credentials for your role session.

&nbsp;

> AWS Service Role: A role that a service assumes to perform actions in your account on your behalf. When you set up some AWS service environments, you must define a role for the service to assume. This service role must include all the permissions required for the service to access the AWS resources that it needs.

&nbsp;

> AWS service-linked role: A unique type of service role that is linked directly to an AWS service. Service-linked roles are predefined by the service and include all the permissions that the service requires to call other AWS services on your behalf. The linked service also defines how you create, modify, and delete a service-linked role. A service might automatically create or delete the role.

&nbsp;

> AWS service role for an EC2 instance: A special type of service role that an application running on an Amazon EC2 instance can assume to perform actions in your account. This role is assigned to the EC2 instance when it is launched. Applications running on that instance can retrieve temporary security credentials and perform actions that the role allows.

-AWS-[Roles Terms and Concepts](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html)

### Attribute Based Access Control (ABAC)

> Attribute-based access control (ABAC) is an authorization strategy that defines permissions based on attributes. In AWS, these attributes are called tags. Tags can be attached to IAM principals (users or roles) and to AWS resources. You can create a single ABAC policy or small set of policies for your IAM principals. These ABAC policies can be designed to allow operations when the principal's tag matches the resource tag. ABAC is helpful in environments that are growing rapidly and helps with situations where policy management becomes cumbersome.

-AWS-[What Is ABAC for AWS?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html)

### Operations

> Then you can review the last accessed information for your users or groups to learn when your users last attempted to access the services that your PowerUserExampleCorp policy allows.

-AWS-[Creating Your First IAM Delegated User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-delegated-user.html)

### Federation

> Your users might already have identities outside of AWS, such as in your corporate directory. If those users need to work with AWS resources (or work with applications that access those resources), then those users also need AWS security credentials. You can use an IAM role to specify permissions for users whose identity is federated from your organization or a third-party identity provider (IdP).

![Federation](federated.png)

* Federating Users of a Mobile or Web-based App with Amazon Cognito

* Federating Users with Public Identity Service Providers or OpenID Connect

* Federating users with SAML 2.0

* Federating users by creating a custom identity broker application

-AWS-[Providing Access to Externally Authenticated Users (Identity Federation)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_federated-users.html)

### Permission Boundary

> AWS supports permissions boundaries for IAM entities (users or roles). A permissions boundary is an advanced feature for using a managed policy to set the maximum permissions that an identity-based policy can grant to an IAM entity. An entity's permissions boundary allows it to perform only the actions that are allowed by both its identity-based policies and its permissions boundaries.

-AWS-[Permissions Boundaries for IAM Entities](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html)

### NotAction

> NotAction is an advanced policy element that explicitly matches everything except the specified list of actions. Using NotAction can result in a shorter policy by listing only a few actions that should not match, rather than including a long list of actions that will match.

-AWS-[IAM JSON Policy Elements: NotAction](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_notaction.html)

### A Cloud Guru

![ARN](arn.png)

![Policy](policy.png)

Users can use MFA with CLI, but requires using sts get-session-token.  Can then enforce that all API calls include MFA, including from CLI.

IAM includes a "Credential Report" that can be used to determine if users have MFA.

## Exercises

### Secure Account

Check boxes, e.g., MFA

### Create New User

1. Create User with no permissions

2. Review content of downloadable CSV file, e.g., keys

### Add New User to Group

1. Add new User to *Administrators* group

2. Observe *AdministratorAccess* Policy

### Create Policy

#### Assumptions

This assumes we have created two S3 buckets, a and b, (do not need to really understand) and uploaded a file into each.

#### Tasks

1. Create Policy; with properties

2. Observe Policy JSON

3. Remove new User from *Administrators* group

4. Add *my-policy* to new User

5. Login as New User; confirm can List two Buckets, but cannot see full list of Buckets nor can open a file

6. Login back in as administrator and observe use of Policy using Access Advisor

Properties

* Name: my-policy

* Service: S3

* Action: ListBucket

* Resources: All

### Deny Statement

1. Update *my-policy* with an expicit ListBucket Deny on Bucket b

2. Login as New User; confirm can only list a Bucket

### Create Role

1. Create Role *super-user* with trust relationship to same account with permission *AdministratorAccess*

2. Create inline policy named *super-user* for user with: STS, Write (AssumeRole), Role ARN

3. Login as user and switch roles and confirm access

#### Supplemental Tasks

1. Delete new user

2. Delete *super-user* Role

3. Delete *my-policy* Policy

### Create Service Role

1. Create Role, *my-s3-reader* for EC2 with policy *AmazonS3ReadyOnlyAccess*

2. Create EC2 Instance with Role *my-s3-reader*

3. Login to EC2 Instance and run *aws s3 ls*

#### Suplemental Tasks

1. Delete EC2 Instance

2. Delete *my-s3-reader* Role
