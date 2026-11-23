### AWS CloudFormation

AWS CloudFormation is an Infrastructure as Code (IaC) service that lets you model, provision, and manage AWS and third-party resources using declarative JSON or YAML templates. Instead of configuring services manually, you define your desired setup in code and deploy related resources together as a single unit.

- It allows you to define AWS resources like EC2 instances, S3 buckets, RDS databases, and networking components in code templates.
- Automates the provisioning and deployment process, eliminating the need to manually configure resources in the AWS Console.
- Ensures infrastructure consistency by creating identical environments across multiple regions or accounts using the same template.
- Supports version control and change management, allowing you to track modifications, roll back updates, and maintain reliable infrastructure.
- When you use CloudFormation, you work with templates and stacks. You create templates to describe your AWS resources and their properties. Whenever you create a stack, CloudFormation provisions the resources that are described in your template.

**Core Concepts of AWS CloudFormation** :

- _**Templates**_ : An AWS CloudFormation template is a declarative JSON or YAML text file that defines the AWS resources you want to provision, update, and manage together as a single unit called a stack. You can save these files with any extension, such as .yaml, .json, .template, or .txt. CloudFormation uses these templates as blueprints for building your AWS resources. For example, in a template, you can describe an Amazon EC2 instance, such as the instance type, the AMI ID, block device mappings, and its Amazon EC2 key pair name. Whenever you create a stack, you also specify a template that CloudFormation uses to create whatever you described in the template.

- _**Stacks**_ : A collection of AWS resources created, updated, and deleted together from a template as one manageable unit. When you use CloudFormation, you manage related resources as a single unit called a stack. You create, update, and delete a collection of resources by creating, updating, and deleting stacks.
  - All the resources in a stack are defined by the stack's CloudFormation template. Suppose you created a template that includes an Auto Scaling group, Elastic Load Balancing load balancer, and an Amazon Relational Database Service (Amazon RDS) database instance. To create those resources, you create a stack by submitting the template that you created, and CloudFormation provisions all those resources for you.

- _**Change Sets**_ : Previews of proposed modifications to a stack so you can check for risky updates or resource replacements before applying them. If you need to make changes to the running resources in a stack, you update the stack.
  - Before making changes to your resources, you can generate a change set, which is a summary of your proposed changes. Change sets allow you to see how your changes might impact your running resources, especially for critical resources, before implementing them.
  - For example, if you change the name of an Amazon RDS database instance, CloudFormation will create a new database and delete the old one. You will lose the data in the old database unless you've already backed it up. If you generate a change set, you will see that your change will cause your database to be replaced, and you will be able to plan accordingly before you update your stack.
  - _Updating a stack with a change set_ : When you need to update your stack's resources, you can modify the stack's template. You don't need to create a new stack and delete the old one. To update a stack, create a change set by submitting a modified version of the original stack template, different input parameter values, or both.
    - CloudFormation compares the modified template with the original template and generates a change set. The change set lists the proposed changes. After reviewing the changes, you can start the change set to update your stack or you can create a new change set. The following diagram summarizes the workflow for updating a stack:

    ![CloudFormationChangeSet](https://docs.aws.amazon.com/images/AWSCloudFormation/latest/UserGuide/images/update-stack-diagram.png)

- _**Drift Detection**_ : AWS CloudFormation drift detection identifies whether your stack’s actual live resources have deviated from their expected template configurations due to out-of-band changes (such as manual edits in the AWS Management Console or CLI).
  - How It Works & Drift Statuses :-
    - CloudFormation compares the current property values of supported resources against the values explicitly defined in your template.
    - Stack Drift Statuses : A stack is marked as IN_SYNC if all supported resources match the template, DRIFTED if at least one resource differs, or NOT_CHECKED if drift detection hasn't been run.
    - Resource Drift Statuses : Individual resources report as IN_SYNC, MODIFIED (properties changed), DELETED (removed outside CloudFormation), or NOT_CHECKED (unsupported resource type or skipped).
    - Property Differences : For modified resources, CloudFormation highlights exact JSON/YAML diffs categorized as ADD, REMOVE, or NOT_EQUAL.

- **How CloudFormation works** : When you use CloudFormation to create your stack, CloudFormation makes underlying service calls to AWS to provision and configure the resources described in your template. You need permission to create these resources. For example, to create EC2 instances by using CloudFormation, you need permissions to create instances.
  - The calls that CloudFormation makes are all declared by your template. For example, suppose you have a template that describes an EC2 instance with a t2.micro instance type.
  - When you use that template to create a stack, CloudFormation calls the Amazon EC2 create instance API and specifies the instance type as t2.micro. The following diagram summarizes the CloudFormation workflow for creating stacks.

  ![AWSCloudFormation](https://docs.aws.amazon.com/images/AWSCloudFormation/latest/UserGuide/images/create-stack-diagram.png)

- Before provisioning resources, CloudFormation runs pre-deployment validation on your template. This checks for common errors such as invalid property syntax and resource name conflicts. If validation fails, the operation stops before any resources are created. Validation runs automatically on all Create Stack, Update Stack, and Create Change Set operations. To skip validation, you can use the _DisableValidation_ parameter.
- After all the resources have been created, CloudFormation reports that your stack has been created. You can then start using the resources in your stack. If stack creation fails, CloudFormation rolls back your changes by deleting the resources that it created.

- _**Deployment time**_ : How long a stack operation takes depends on the resources in the stack. CloudFormation provisions independent resources in parallel and moves forward as soon as each resource is ready. In workloads that include resources such as database instances, load balancers, or NAT gateways, those resources take longer to become ready to serve traffic and account for most of the deployment time.

- _**Express mode**_ : For faster stack operations during development, use express mode. Express mode completes stack operations as soon as CloudFormation applies the resource configuration, without waiting for resources to fully stabilize.

### AWS Cloud Development Kit

The AWS Cloud Development Kit (AWS CDK) is an open-source framework for defining cloud infrastructure as code using programming languages and provisioning it via AWS CloudFormation. It supports TypeScript, JavaScript, Python, Java, C#/.NET, and Go.

- **Some key concepts** :
  - Apps and Stacks : An app groups one or more stacks, which act as deployable units mapped to an AWS account and Region.
  - Constructs : Reusable building blocks representing cloud components across three levels :-
    - L1 (Cfn) : Direct mappings to underlying CloudFormation resources.
    - L2 : Curated constructs with sensible defaults, helper methods, and automatic IAM permissions.
    - L3 (Patterns) : Multi-resource architectural patterns for common workflows.
  - CDK Blocks : An expansion that packages infrastructure constructs alongside application code and local implementations for capabilities like databases, authentication, file storage, and AI agents.
