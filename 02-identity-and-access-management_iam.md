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
