# IAM: Identity and Access Management

When accessing AWS, the root account should **never** be used. Users must be created with the proper permissions. IAM is central to AWS.
- Users: A physical person
- Groups: Functions (admin, devops) Teams (engineering, design) which contain a group of users
- Roles: Internal usage within AWS resources
- Policies (JSON documents): Defines what each of the above can and cannot do. **Note**: IAM has predefined managed policies.


### For big enterprises:
- IAM Federation: Integrate their own repository of users with IAM using SAML standard

## Policies
IAM policies define permissions for an action regardless of the method that you use to perform the operation.

### Policy components
[AWS document](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
Poplicy is present by JSON format. For examples:
```
 {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "Stmt1571666184581",
          "Action": [
            "elasticbeanstalk:CreateApplication"
          ],
          "Effect": "Allow",
          "Resource": "arn:aws:elasticbeanstalk:ap-southeast-1:1234567:application/staging",
          "Condition": {
            "DateGreaterThan": {
              "aws:CurrentTime": "2019/10/18"
            }
          }
        }
      ]
    }
```

The information in a statement is contained within a series of elements.

* **Version** – Specify the version of the policy language that you want to use. We recommend that you use the latest 2012-10-17 version. For more information, see IAM JSON policy elements: Version
* **Statement** – Use this main policy element as a container for the following elements. You can include more than one statement in a policy.
* **Sid** (Optional) – Include an optional statement ID to differentiate between your statements
* **Effect** – Use Allow or Deny to indicate whether the policy allows or denies access.
* **Principal** (Required in only some circumstances) – If you create a resource-based policy, you must indicate the account, user, role, or federated user to which you would like to allow or deny access. If you are creating an IAM permissions policy to attach to a user or role, you cannot include this element. The principal is implied as that user or role.
* **Action** – Include a list of actions that the policy allows or denies.
* **Resource** (Required in only some circumstances) – If you create an IAM permissions policy, you must specify a list of resources to which the actions apply. If you create a resource-based policy, this element is optional. If you do not include this element, then the resource to which the action applies is the resource to which the policy is attached
* **Condition** (Optional) – Specify the circumstances under which the policy grants permission.

### Policy types
- **Identity-based policies**
  - Attach managed and inline policies to IAM identities (users, groups to which users belong, or roles). Identity-based policies grant permissions to an identity.

- **Resource-based policies**
  - Attach inline policies to resources. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies. Resource-based policies grant permissions to a principal entity that is specified in the policy. Principals can be in the same account as the resource or in other accounts.
  - **Trust policy**: Trust policies define which principal entities (accounts, users, roles, and federated users) can assume the role. An IAM role is both an identity and a resource that supports resource-based policies. For this reason, you must attach both a trust policy and an identity-based policy to an IAM role. The IAM service supports only one type of resource-based policy called a role trust policy, which is attached to an IAM role

- **Permissions boundaries**
  - Use a managed policy as the permissions boundary for an IAM entity (user or role). That policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions. Permissions boundaries do not define the maximum permissions that a resource-based policy can grant to an entity.

- **Organizations SCPs**
  - Use an AWS Organizations service control policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.

- **Access control lists (ACLs)**
  - Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure. ACLs are cross-account permissions policies that grant permissions to the specified principal entity. ACLs cannot grant permissions to entities within the same account.

- **Session policies**
  - Pass advanced session policies when you use the AWS CLI or AWS API to assume a role or a federated user. Session policies limit the permissions that the role or user's identity-based policies grant to the session. Session policies limit permissions for a created session, but do not grant permissions. For more information, see [Session Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_session).

- **AWS Organizations Service Control Policies (SCP)**
  - If you enable all features of AWS organization, then you can apply service control policies (SCPs) to any or all of your accounts. SCPs are JSON policies that specify the maximum permissions for an organization or organizational unit (OU). The SCP limits permissions for entities in member accounts, including each AWS account root user. An explicit deny in any of these policies overrides the allow.


### AWS Policy Simulator
- When creating new custom policies you can test it here:
  - https://policysim.aws.amazon.com/home/index.jsp
  - This policy tool can you save you time in case your custom policy statement's permission is denied
- Alternatively, you can use the CLI:
    - Some AWS CLI commands (not all) contain `--dry-run` option to simulate API calls. This can be used to test permissions.
    - If the command is successful, you'll get the message: `Request would have succeeded, but DryRun flag is set`
    - Otherwise, you'll be getting the message: `An error occurred (UnauthorizedOperation) when calling the {policy_name} operation`
  
### Best practices:
- One IAM User per person **ONLY**
- One IAM Role per Application
- IAM credentials should **NEVER** be shared
- Never write IAM credentials in your code. **EVER**
- Never use the ROOT account except for initial setup
- It's best to give users the minimal amount of permissions to perform their job

## Access Analyzer
IAM Access Analyzer simplifies inspecting unused access to guide you toward least privilege. Security teams can use IAM Access Analyzer to gain visibility into unused access across their AWS organization and automate how they rightsize permissions. When the unused access analyzer is enabled, IAM Access Analyzer continuously analyzes your accounts to identify unused access and creates a centralized dashboard with findings. The findings highlight unused roles, unused access keys for IAM users, and unused passwords for IAM users. For active IAM roles and users, the findings provide visibility into unused services and actions.

## AWS Trusted Advisor
AWS Trusted Advisor is an online tool that provides you real-time guidance to help you provision your resources following AWS best practices on cost optimization, security, fault tolerance, service limits, and performance improvement.

## Amazon Inspector
Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS. Amazon Inspector automatically assesses applications for exposure, vulnerabilities, and deviations from best practices.

## AWS Security Hub
AWS Security Hub provides you with a comprehensive view of your security state in AWS and helps you assess your AWS environment against security industry standards and best practices.