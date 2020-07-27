# AWS Control Tower

## Concepts

> AWS Control Tower provides the easiest way to set up and govern a secure, compliant, multi-account AWS environment based on best practices established by working with thousands of enterprises. With AWS Control Tower, end users on your distributed teams can provision new AWS accounts quickly. Meanwhile your central cloud administrators will know that all accounts are aligned with centrally established, company-wide compliance policies.

&nbsp;

> The structure of a landing zone in AWS Control Tower is as follows:

* Root – The parent that contains all other OUs in your landing zone.

* Core OU – This OU contains the log archive and audit member accounts. These accounts often are referred to as shared accounts.

* Custom OU – The custom OU is created when you launch your landing zone. This and other member OUs contain the member accounts that your users work with to perform their AWS workloads.

* AWS SSO directory – This directory houses your AWS SSO users. It defines the scope of permissions for each AWS SSO user.

* AWS SSO users – These are the identities that your users can assume to perform their AWS workloads in your landing zone.

> In AWS Control Tower, three shared accounts in your landing zone are not provisioned in Account Factory: the master account, the log archive account, and the audit account.

* Master Account: This is the account that you created specifically for your landing zone. This account is used for billing for everything in your landing zone. It's also used for Account Factory provisioning of accounts, as well as to manage OUs and guardrails.

* Log Archive Account: This account works as a repository for logs of API activities and resource configurations from all accounts in the landing zone.

* Audit Account: The audit account is a restricted account that's designed to give your security and compliance teams read and write access to all accounts in your landing zone. 

> A guardrail is a high-level rule that provides ongoing governance for your overall AWS environment. Each guardrail enforces a single rule, and it's expressed in plain language. Compliance needs evolve, and you can change the elective or strongly recommended guardrails that are in force, at any time, from the AWS Control Tower console. Mandatory guardrails are always applied, and they can't be changed.

&nbsp;

> Preventive guardrails prevent actions from occurring.

&nbsp;

> Detective guardrails detect specific events when they occur and log the action in CloudTrail.

&nbsp;

> When you create a landing zone, the region that you're using for access to the AWS Management Console becomes your home AWS Region for AWS Control Tower.

&nbsp;

> Currently, all preventive guardrails work globally. Detective guardrails, however, only work in regions where AWS Control Tower is supported.

-AWS-[What Is AWS Control Tower?](https://docs.aws.amazon.com/controltower/latest/userguide/what-is-control-tower.html)

> The preventive guardrails are implemented using Service Control Policies (SCPs), which are part of AWS Organizations.

&nbsp;

> The detective guardrails are implemented using AWS Config rules and AWS Lambda functions.

-AWS-[Guardrails in AWS Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/guardrails.html)

> AWS Control Tower creates a customer's account by calling the CreateAccount API of AWS Organizations. When AWS Organizations creates this account, it creates a role within that account, which AWS Control Tower names by passing in a parameter to the API. The name of the role is AWSControlTowerExecution.

-AWS-[What Is AWS Control Tower?](https://docs.aws.amazon.com/controltower/latest/userguide/what-is-control-tower.html)

> The VPC created by AWS Control Tower when you provision an account in Account Factory is not the same as the AWS default VPC.

&nbsp;

> When AWS Control Tower sets up a new account in a supported AWS Region, AWS Control Tower automatically deletes the default AWS VPC, and it sets up a new VPC configured by AWS Control Tower.

-AWS-[AWS Control Tower and VPCs](AWS Control Tower and VPCs)

## Exercises

[Getting Started with AWS Control Tower](https://docs.aws.amazon.com/controltower/latest/userguide/getting-started-with-control-tower.html)
