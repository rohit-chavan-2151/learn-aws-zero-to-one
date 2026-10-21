## **AWS IAM (Identity & Access Management)**

AWS Identity and Access Management (IAM) is a core security service in Amazon Web Services that controls who can sign in and what actions they can perform on your cloud resources. It manages authentication _(who can sign in)_, authorization _(what actions they are allowed to perform)_, and least-privilege permissions across your account at no extra cost. Below are some core components of IAM :

- **IAM Users** : Individual people or applications with long-term credentials like passwords or access keys.
- **IAM Groups** : Collections of users that share a set of specific permissions to make management easier.
- **IAM Roles** : Sets of temporary permissions that trusted entities, applications, or AWS services can assume.
- **IAM Policies** : JSON documents that define explicit allow or deny rules for specific actions and resources. Below are the types of IAM Policies:
  - **AWS-Managed Policies** : Policies created and maintained by AWS for common use cases.
  - **Customer-Managed Policies** : Custom policies created and managed by users based on organizational requirements.
  - **Inline Policies** : Policies embedded directly into a single IAM user, group, or role.
  - **Resource-Based Policies** : Policies attached directly to AWS resources such as S3 bucket policies.

_**Workflow of IAM**_ : Identity and Access Management (IAM) works by clearly defining who can access AWS, what they can access, and under what conditions. Its working can be understood in the following flow:

![workflowOfIAM](https://media.geeksforgeeks.org/wp-content/uploads/20260608163749217807/IAM-aws.webp)

1. **Identify the User or Entity (Who)** : IAM first identifies who is requesting access. This could be: An IAM user (human), An application or service. An AWS service assuming a role
2. **Authenticate the Request** : IAM verifies the identity using authentication mechanisms like, Username and password, Access keys, Multi-Factor Authentication (MFA) (Only authenticated identities can proceed further.)
3. **Authorize Using Policies (Can Access)** : After authentication, IAM checks policies attached to the user, group, or role. These policies define:
   Allowed or denied actions (e.g., s3:GetObject), Specific resources (e.g., a particular S3 bucket), Conditions (time, IP address, MFA usage)
4. **Evaluate Permissions** : IAM evaluates permissions in this order:

- Explicit Deny: always blocks access
- Explicit Allow: grants access
- Implicit Deny: default if no allow exists
  Access is granted only if an explicit allow exists and no deny overrides it.

5. **Grant Access to Resources (What)** :If authorization succeeds, IAM allows the user or service to perform the requested action on the specified AWS resource such as: EC2 instances, S3 buckets, RDS databases

6. **Temporary Access via Roles (Optional but Recommended)** : For applications and services, IAM roles provide temporary credentials instead of long-term keys, improving security and reducing credential misuse.

- _**Federation and Single Sign-On (SSO)**_ : Federation allows external users to access AWS using existing identity providers. It supports corporate directories and social logins. Enables Single Sign-On (SSO). Reduces password fatigue and improves security.
- _**Role-Based Access Control (RBAC)**_ : RBAC assigns permissions based on job roles rather than individual users. It simplifies access control, aligns permissions with organizational structure and minimizes security risks caused by excess privileges.

**IAM Permissions** : Users or Groups can be assigned JSON documents called policies. These policies define the permissions of the users. In AWS you apply the least privilege principle: don’t give more permissions than a user needs.

![IAMPernissions](https://miro.medium.com/0*2qvQJOBLk8HEDQNd)

**IAM Policies Inheritance** : IAM policy inheritance is the process where permissions flow down from parent containers or groups to chi ld resources or members.

- _Group Inheritance_ : Users added to an IAM group automatically inherit all permissions attached to that group while keeping their own direct-user policies.
- _Organization & SCPs_ : AWS Organizations allows declarative policies or Service Control Policies (SCPs) to flow from the Root down through Organizational Units (OUs) to individual AWS Accounts.
- _Additive Nature_ : Permissions are generally additive; an explicit Deny anywhere in the evaluation chain will override any Allow.

![IAMInheritance](https://kananinirav.com/images/IAM_Policies_inheritance.png)

**IAM Policies Structure** : It consists of,

- Version : policy language version, always include “2012-10-17”
- Id : an identifier for the policy (optional)
- Statement : one or more individual statements (required). The statement consists of,
  - Sid : an identifier for the statement (optional)
  - Effect : whether the statement allows or denies access (Allow, Deny)
  - Principal : account/user/role to which this policy applied to
  - Action : list of actions this policy allows or denies
  - Resource : list of resources to which the actions applied to
  - Condition : conditions for when this policy is in effect (optional)

![IAMPolicyStructure](https://sonraisecurity.com/wp-content/uploads/Screenshot-2023-08-14-at-12.47.05-PM.png)

**Multi Factor Authentication - MFA** : Users have access to your account and can possibly change configurations or delete resources in your AWS account. You want to protect your Root Accounts and IAM users. MFA = _password you know_ + _security device you own_

- Main benefit of MFA : if a password is stolen or hacked, the account is not compromised
- The MFA device options can be a Virtual MFA device like Google Authenticator App (Support for multiple tokens on a single device) or Universal 2nd Factor (U2F) Security Key (Support for multiple root and IAM users using a single security key)

**Users Access in AWS** : To access AWS, you have three options,

- AWS Management Console (protected by password + MFA)
- AWS Command Line Interface (CLI): protected by access keys
- AWS Software Developer Kit (SDK) - for code: protected by access keys
  - Access Keys are generated through the AWS Console. Users can manage their own access keys. Access Keys are secret, just like a password.

**AWS CLI (Command Line Interface)** : A tool that enables you to interact with AWS services using commands in your command-line shell. Direct access to the public APIs of AWS services. You can develop scripts to manage your resources

**AWS SDK (Software Development Kit)** : They are Language-specific APIs (set of libraries). Enables you to access and manage AWS services
programmatically. They are embedded within your application.

- It supports - SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)
- Mobile SDKs (Android, iOS, …)
- IoT Device SDKs (Embedded C, Arduino, …)

**AWS IAM Roles for services** : They allow AWS workloads, EC2 instances, or Kubernetes pods to assume temporary, least-privilege credentials. They eliminate hardcoded long-term keys by using a combination of trust policies and permission policies managed via standard service roles or service-linked roles. Core Role Types for Services are,

- AWS Service Roles : Custom roles created by administrators that an AWS service assumes to perform actions on your behalf.
- Service-Linked Roles (SLRs) : Predefined, unmodifiable roles owned directly by an AWS service (like Auto Scaling or RDS) with pre-configured permissions.
- IAM Roles for Service Accounts (IRSA) : Used in Amazon EKS to let Kubernetes pods assume AWS IAM roles using OpenID Connect (OIDC) tokens.

**IAM Security Tools** :

- IAM Credentials Report (account-level): A report that lists all your account's users and the status of their various credentials.
- IAM Access Advisor (user-level) : Access advisor shows the service permissions granted to a user and when those services were last accessed. You can use this information to revise your policies.

![SharedResponsibilityIAM](https://miro.medium.com/v2/resize:fit:1400/1*6WCsTAWD4AidBsflS2lufw.png)
