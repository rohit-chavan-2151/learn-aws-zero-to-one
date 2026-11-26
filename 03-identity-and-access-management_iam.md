## **AWS IAM (Identity & Access Management)**

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can manage permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources. IAM provides the infrastructure necessary to control authentication and authorization for your AWS accounts. Here, authentication means _(who can sign in)_, and authorization means _(what actions they are allowed to perform)_. You must always provide least-privilege permissions across your account at no extra cost. Below are some core components of IAM :

- **Some key features** :-
  - _Identities_ : When you create an AWS account, you begin with one sign-in identity called the AWS account root user that has complete access to all AWS services and resources. We strongly recommend that you don't use the root user for everyday tasks. You must use IAM to set up other identities in addition to your root user, such as administrators, analysts, and developers, and grant them access to the resources they need to succeed in their tasks.
  - _Access management_ : After a user is set up in IAM, they use their sign-in credentials to authenticate with AWS. Authentication is provided by matching the sign-in credentials to a principal (an IAM user, AWS STS federated principal, IAM role, or application) trusted by the AWS account.
    - Next, a request is made to grant the principal access to resources. Access is granted in response to an authorization request if the user has been given permission to the resource. For example, when you first sign in to the console and are on the console Home page, you aren't accessing a specific service. When you select a service, the request for authorization is sent to that service and it looks to see if your identity is on the list of authorized users, what policies are being enforced to control the level of access granted, and any other policies that might be in effect.
    - Authorization requests can be made by principals within your AWS account or from another AWS account that you trust.
    - Once authorized, the principal can take action or perform operations on resources in your AWS account. For example, the principal could launch a new Amazon Elastic Compute Cloud instance, modify IAM group membership, or delete Amazon Simple Storage Service buckets.
  - _Service availability_ : IAM achieves high availability by replicating data across multiple servers within Amazon's data centers around the world. If a request to change some data is successful, the change is committed and safely stored. However, the change must be replicated across IAM, which can take some time. Such changes include creating or updating users, groups, roles, or policies.

- **How IAM works** : AWS Identity and Access Management provides the infrastructure necessary to control authentication and authorization for your AWS account.
  - First, a human user or an application uses their sign-in credentials to authenticate with AWS. IAM matches the sign-in credentials to a principal (an IAM user, AWS STS federated user principal, IAM role, or application) trusted by the AWS account and authenticates the principal to access AWS.
  - Next, IAM makes a request to grant the principal access to resources. IAM grants or denies access in response to an authorization request. For example, when you first sign in to the console and are on the console Home page, you aren't accessing a specific service. When you select a service, you send an authorization request to IAM for that service. IAM verifies that your identity is on the list of authorized users, determines what policies control the level of access granted, and evaluates any other policies that might be in effect. Principals(Users) within your AWS account or from another AWS account that you trust can make authorization requests.
  - Once authorized, the principal can perform actions or operations on resources in your AWS account. For example, the principal could launch a new Amazon Elastic Compute Cloud instance, modify IAM group membership, or delete Amazon Simple Storage Service buckets.

- **Components of a request** : When a principal tries to use the AWS Management Console, the AWS API, or the AWS CLI, that principal sends a request to AWS. The request includes the following information:
  - _Actions or operations_ – The actions or operations that the principal wants to perform, such as an action in the AWS Management Console, or an operation in the AWS CLI or AWS API.
  - _Resources_ – The AWS resource object upon which the principal requests to perform an action or operation.
  - _Principal_ – The person or application that used an entity (user or role) to send the request. Information about the principal includes the permission policies.
  - _Environment data_ – Information about the IP address, user agent, SSL enabled status, and the timestamp.
  - _Resource data_ – Data related to the resource requested, such as a DynamoDB table name or a tag on an Amazon EC2 instance.
- AWS gathers the request information into a request context, which IAM evaluates to authorize the request.

### Core Concepts in IAM :

- **IAM Account Root User** : When you first create an Amazon Web Services (AWS) account, you begin with a single sign-in identity that has complete access to all AWS services and resources in the account. This identity is called the AWS account root user. The email address and password that you used to create your AWS account are the credentials you use to sign in as your root user.
- **IAM Users** : An IAM user is an entity that you create in your AWS account. The IAM user represents the human user or workload who uses the IAM user to interact with AWS resources. An IAM user consists of a name and credentials. An IAM user with administrator permissions is not the same thing as the AWS account root user.
  - You can access AWS in different ways depending on the IAM user credentials like console password, access keys, SSH keys, etc.
  - You can choose the credentials that are right for your IAM user. When you use the AWS Management Console to create an IAM user, you must choose to at least include a console password or access keys.
  - By default, a new IAM user has no permissions to do anything. They are not authorized to perform any AWS operations or to access any AWS resources.
    - An advantage of having individual IAM users is that you can assign permissions individually to each user. You might assign administrative permissions to a few users, who then can administer your AWS resources and can even create and manage other IAM users. In most cases, however, you want to limit a user's permissions to just the tasks (AWS actions or operations) and resources that are needed for the job.
  - You can also add a permissions boundary to your IAM users. A permissions boundary is an advanced feature that allows you to use AWS managed policies to limit the maximum permissions that an identity-based policy can grant to an IAM user or role.
- **IAM User Groups** : An IAM user group is a collection of IAM users. User groups let you specify permissions for multiple users, which can make it easier to manage the permissions for those users.
  - For example, you could have a user group called Admins and give that user group typical administrator permissions. Any user in that user group automatically has Admins group permissions. If a new user joins your organization and needs administrator privileges you can assign the appropriate permissions by adding the user to the Admins user group. If a person changes jobs in your organization, instead of editing that user's permissions you can remove them from the old IAM groups and add them to the appropriate new IAM groups.
  - You can attach an identity-based policy to a user group so that all of the users in the user group receive the policy's permissions. You cannot identify a user group as a _Principal_ in a policy (such as a resource-based policy) because groups relate to permissions, not authentication, and principals are authenticated IAM entities. Below are some characterstics of IAM group,
    - A user group can contain many users, and a user can belong to multiple user groups.
    - User groups can't be nested; they can contain only users, not other IAM groups.
    - There is no default user group that automatically includes all users in the AWS account. If you want to have a user group like that, you must create it and assign each new user to it.
    - The number and size of IAM resources in an AWS account, such as the number of groups, and the number of groups that a user can be a member of, are limited.
- **IAM Roles** : IAM roles are cloud identities that grant temporary security credentials so trusted users, applications, or services can access resources without long-term passwords or access keys. Instead of being tied to a single person or permanent key, a role is assumed when needed and expires automatically.
  - An IAM role is an IAM identity that you can create in your account that has specific permissions. An IAM role is similar to an IAM user, in that it is an AWS identity with permission policies that determine what the identity can and cannot do in AWS.
  - However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it. Also, a role does not have standard long-term credentials such as a password or access keys associated with it. Instead, when you assume a role, it provides you with temporary security credentials for your role session.
  - You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources. For example, you might want to grant users in your AWS account access to resources they don't usually have, or grant users in one AWS account access to resources in another account.
  - _Common scenarios for IAM roles_ : As with most AWS features, you generally have two ways to use a role: interactively in the IAM console, or programmatically with the AWS CLI, Tools for Windows PowerShell, or API.
    - IAM users in your account using the IAM console can switch to a role to temporarily use the permissions of the role in the console. The users give up their original permissions and take on the permissions assigned to the role. When the users exit the role, their original permissions are restored.
    - An application or a service offered by AWS (like Amazon EC2) can assume a role by requesting temporary security credentials for a role with which to make programmatic requests to AWS. You use a role this way so that you don't have to share or maintain long-term security credentials (for example, by creating an IAM user) for each entity that requires access to a resource.
    - The simplest way to use roles is to grant your IAM users permissions to switch to roles that you create within your own or another AWS account. They can switch roles easily using the IAM console to use permissions that you don't ordinarily want them to have, and then exit the role to surrender those permissions. This can help prevent accidental access to or modification of sensitive resources.
    - For more complex uses of roles, such as granting access to applications and services, or federated external users, you can call the _AssumeRole_ API. This API call returns a set of temporary credentials that the application can use in subsequent API calls. Actions attempted with the temporary credentials have only the permissions granted by the associated role. An application doesn't have to "exit" the role the way a user in the console does; rather the application simply stops using the temporary credentials and resumes making calls with the original credentials.
- **IAM Policies and Permissions** : Manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources. A policy is an object in AWS that, when associated with an identity or resource, defines their permissions.
  - AWS evaluates these policies when an IAM principal (user or role) makes a request. Permissions in the policies determine whether the request is allowed or denied. Most policies are stored in AWS as JSON documents.
  - AWS supports ten types of policies: identity-based policies, resource-based policies, VPC endpoint policies, permissions boundaries, AWS Organizations service control policies (SCPs), AWS Organizations resource control policies (RCPs), access control lists (ACLs), AWS Resource Access Manager (AWS RAM) resource shares, session policies, and scope down policies.

- **IAM Policy Types** : The following policy types, listed in order from most frequently used to less frequently used, are available for use in AWS.
  - **Identity-based policies** : Identity-based policies are JSON permissions policy documents that control what actions an identity (users, groups of users, and roles) can perform, on which resources, and under what conditions. Identity-based policies can be further categorized:
    - _Managed policies_ – Standalone identity-based policies that you can attach to multiple users, groups, and roles in your AWS account. There are two types of managed policies:
      - _AWS managed policies_ – Managed policies that are created and managed by AWS.
      - _Customer managed policies_ – Managed policies that you create and manage in your AWS account. Customer managed policies provide more precise control over your policies than AWS managed policies.
    - _Inline policies_ – Policies that you add directly to a single user, group, or role. Inline policies maintain a strict one-to-one relationship between a policy and an identity. They are deleted when you delete the identity.
  - **Resource-based policies** : Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket. These policies grant the specified principal permission to perform specific actions on that resource and defines under what conditions this applies. Resource-based policies are inline policies. There are no managed resource-based policies.
  - **VPC endpoint policies** : A VPC endpoint policy is a resource-based policy that you attach to a VPC endpoint to control which principals can use the endpoint and which resources can be accessed through it. VPC endpoint policies do not override or replace identity-based policies or resource-based policies attached to the destination service—they act as an additional access boundary scoped to traffic that traverses the endpoint.
  - **IAM permissions boundaries** : A permissions boundary is an advanced feature in which you set the maximum permissions that an identity-based policy can grant to an IAM entity. When you set a permissions boundary for an entity, the entity can perform only the actions that are allowed by both its identity-based policies and its permissions boundaries.
  - **Access control lists (ACLs)** : Access control lists (ACLs) are service policies that allow you to control which principals in another account can access a resource. ACLs cannot be used to control access for a principal within the same account. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document format.
  - **Session policies** : Session policies are advanced policies that you pass as a parameter when you programmatically create a temporary session for a role or an AWS STS federated user principal. The permissions for a session are the intersection of the identity-based policies for the IAM entity (user or role) used to create the session and the session policies. Permissions can also come from a resource-based policy. An explicit deny in any of these policies overrides the allow.

**IAM Policies Inheritance** : IAM policy inheritance is the process where permissions flow down from parent containers or groups to chi ld resources or members.

- _Group Inheritance_ : Users added to an IAM group automatically inherit all permissions attached to that group while keeping their own direct-user policies.
- _Organization & SCPs_ : AWS Organizations allows declarative policies or Service Control Policies (SCPs) to flow from the Root down through Organizational Units (OUs) to individual AWS Accounts.
- _Additive Nature_ : Permissions are generally additive; an explicit Deny anywhere in the evaluation chain will override any Allow.

![IAMInheritance](https://kananinirav.com/images/IAM_Policies_inheritance.png)

- **Overview of JSON policies** : Most policies are stored in AWS as JSON documents. Identity-based policies and policies used to set permissions boundaries are JSON policy documents that you attach to a user or role. Resource-based policies are JSON policy documents that you attach to a resource. SCPs and RCPs are JSON policy documents with restricted syntax that you attach to the AWS Organizations' organization root, organizational unit (OU), or an account. ACLs are also attached to a resource, but you must use a different syntax. Session policies are JSON policies that you provide when you assume a role or federated user session.

- **JSON policy document structure** : As illustrated in the following figure, a JSON policy document includes these elements:
  - Optional policy-wide information at the top of the document
  - One or more individual statements

  ![IAMPolicyStructure](https://sonraisecurity.com/wp-content/uploads/Screenshot-2023-08-14-at-12.47.05-PM.png)

The information in a statement is contained within a series of elements.

- Version – Specify the version of the policy language that you want to use. We recommend that you use the latest 2012-10-17 version.
- Statement – Use this main policy element as a container for the following elements. You can include more than one statement in a policy.
- Sid (Optional) – Include an optional statement ID to differentiate between your statements.
- Effect – Use Allow or Deny to indicate whether the policy allows or denies access.
- Principal (Required in some circumstances) – If you create a resource-based policy, you must indicate the account, user, role, or AWS STS federated user principal to which you would like to allow or deny access. If you are creating an IAM permissions policy to attach to a user or role, you cannot include this element. The principal is implied as that user or role.
- Action – Include a list of actions that the policy allows or denies.
- Resource (Required in some circumstances) – If you create an IAM permissions policy, you must specify a list of resources to which the actions apply. If you create a resource-based policy, it depends on the resource you're using as to whether this element is required or not.
- Condition (Optional) – Specify the circumstances under which the policy grants permission.

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

**IAM Security Tools** :

- IAM Credentials Report (account-level): A report that lists all your account's users and the status of their various credentials.
- IAM Access Advisor (user-level) : Access advisor shows the service permissions granted to a user and when those services were last accessed. You can use this information to revise your policies.

![SharedResponsibilityIAM](https://miro.medium.com/v2/resize:fit:1400/1*6WCsTAWD4AidBsflS2lufw.png)
