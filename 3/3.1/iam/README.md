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

![Policy Diagram](policy_summaries_diagram.png)

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

## Exercises

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

Properties

* Name: my-policy

* Service: S3

* Action: ListBucket

* Resources: All

### Deny Statement

1. Update *my-policy* with an expicit ListBucket Deny on Bucket b

2. Login as New User; confirm can only list a Bucket

