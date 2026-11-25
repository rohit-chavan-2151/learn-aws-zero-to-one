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

---

### AWS Cloud Development Kit

The AWS Cloud Development Kit (AWS CDK) is an open-source framework for defining cloud infrastructure as code using programming languages and provisioning it via AWS CloudFormation. It supports TypeScript, JavaScript, Python, Java, C#/.NET, and Go.

- **Some key concepts** :
  - Apps and Stacks : An app groups one or more stacks, which act as deployable units mapped to an AWS account and Region.
  - Constructs : Reusable building blocks representing cloud components across three levels :-
    - L1 (Cfn) : Direct mappings to underlying CloudFormation resources.
    - L2 : Curated constructs with sensible defaults, helper methods, and automatic IAM permissions.
    - L3 (Patterns) : Multi-resource architectural patterns for common workflows.
  - CDK Blocks : An expansion that packages infrastructure constructs alongside application code and local implementations for capabilities like databases, authentication, file storage, and AI agents.

---

### AWS Elastic Beanstalk

- AWS Elastic Beanstalk is a Platform as a Service (PaaS) and orchestration tool that automates the deployment, scaling, and management of web applications on AWS. Instead of manually configuring servers, load balancers, and networks, you upload your application code or container image, and Elastic Beanstalk provisions and manages the underlying AWS infrastructure for you.
- With Elastic Beanstalk you can deploy web applications into the AWS Cloud on a variety of supported platforms. You build and deploy your applications. Elastic Beanstalk provisions Amazon EC2 instances or EKS clusters, configures load balancing, sets up health monitoring, and dynamically scales your environment.

- **Some Core Features** :-
  - Automated Infrastructure : Automatically sets up and manages underlying services like Amazon EC2, Elastic Load Balancing (ELB), Auto Scaling groups, Amazon S3, and CloudWatch.
  - Broad Runtime Support : Supports applications built with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker containers on Linux or Windows servers.
  - Full Resource Control : Unlike more restrictive PaaS platforms, Elastic Beanstalk lets you access and customize the underlying AWS resources (such as changing EC2 instance types or modifying security groups) whenever you need granular control.
  - Deployment Strategies : Supports multiple update methods—including All-at-Once, Rolling, Immutable, and Blue/Green deployments—to minimize downtime during releases.
  - Managed Updates : Automatically applies OS and platform patches during scheduled maintenance windows.

- Elastic Beanstalk offers two modes : _Standard and Cluster_.
  - Beanstalk Standard runs applications directly on Amazon EC2, is highly cost effective when running smaller, or fewer, applications, and supports Windows applications.
  - Beanstalk Cluster runs applications on Amazon EKS and enables faster deployments, faster autoscaling, improved resource utilization when running multiple environments, and managed OpenTelemetry integration.

| Mode          | Underlying Compute              | Best For                                                                                                           |
| ------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Standard Mode | Dedicated Amazon EC2 instances  | Single applications, lightweight workloads, and Windows/.NET apps                                                  |
| Cluster Mode  | Managed Amazon EKS (Kubernetes) | Consolidating multiple containerized apps onto shared infrastructure for faster scaling and bin-packing efficiency |

The following diagram depicts two Beanstalk Standard environments: one web server environment and one worker environment :-

![BeanstalkModes](https://docs.aws.amazon.com/images/elasticbeanstalk/latest/dg/images/aeb-overview.png)

The following diagram depicts two Beanstalk Cluster environments sharing an EKS cluster :-

![BeanstalkCluster](https://docs.aws.amazon.com/images/elasticbeanstalk/latest/dg/images/aeb-overview-cluster.png)

- **Supported Platforms** :
  - Elastic Beanstalk supports applications developed in Go, Java, .NET, Node.js, PHP, Python, and Ruby. Elastic Beanstalk also supports Docker containers, where you can choose your own programming language and application dependencies.
  - When you deploy your application, Elastic Beanstalk builds the selected supported platform version and provisions one or more AWS resources in your AWS account to run your application.
  - With Beanstalk Cluster mode there is no platform involved; you provide a container image, or source that Elastic Beanstalk builds into one.
  - You can interact with Elastic Beanstalk through the Elastic Beanstalk console, the AWS Command Line Interface (AWS CLI), the official GitHub Action, or the EB CLI, a high-level command line tool designed specifically for Elastic Beanstalk. You can also define your environments as infrastructure as code, with AWS CloudFormation (CloudFormation) or with Terraform through the AWS provider.

- **Application deploy workflow** :
  - To use Elastic Beanstalk, you create an application, then upload your application source bundle to Elastic Beanstalk. Next, you provide information about the application, and Elastic Beanstalk automatically launches an environment and creates and configures the AWS resources needed to run your code.
  - After you create and deploy your application and your environment is launched, you can manage your environment and deploy new application versions. Information about the application—including metrics, events, and environment status—is made available through the Elastic Beanstalk console, APIs, and Command Line Interfaces.
  - The following diagram illustrates Elastic Beanstalk workflow :-
    ![BeanstalkWorfflow](https://docs.aws.amazon.com/images/elasticbeanstalk/latest/dg/images/clearbox-flow-00.png)

- It consists of three architecture models :
  i. Single Instance deployment : good for dev
  ii. LB + ASG : great for production or pre-production web applications
  iii. ASG only : great for non-web apps in production (workers, etc..)

- **Difference between AWS Cloudformation & AWS Elastic Beanstalk** :

| Feature                 | AWS Elastic Beanstalk                                                        | AWS CloudFormation                                                     |
| ----------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Primary Role            | Platform as a Service (PaaS) for app deployment                              | Infrastructure as Code (IaC) for resource provisioning                 |
| Main Focus              | Application code, runtimes, and scaling                                      | Defining the exact state of AWS infrastructure                         |
| Scope of Services       | Limited to compute and app-hosting stacks (EC2, ELB, Auto Scaling, RDS, EKS) | Supports virtually every AWS service and resource type                 |
| Configuration Input     | Upload source code/containers + optional .ebextensions or config files       | Declarative YAML or JSON templates                                     |
| Control vs. Convenience | High convenience; abstracts away server setup while keeping basic knobs      | Granular control over every networking, security, and resource setting |
| Target Audience         | Application developers who want minimal infrastructure overhead              | DevOps and systems engineers managing complex cloud architectures      |

- **How They Work Together** : They are not strictly mutually exclusive—in fact, Elastic Beanstalk uses CloudFormation under the hood to spin up the EC2 instances, load balancers, and Auto Scaling groups for your environment. Furthermore, you can write a CloudFormation template to create and manage an Elastic Beanstalk application alongside external resources (like a standalone database, S3 bucket, or custom VPC) in a single repeatable stack.

- **When to Choose Which** :
  - Choose Elastic Beanstalk if you want to deploy a standard web app, API, or Docker container quickly without writing infrastructure templates from scratch.
  - Choose CloudFormation if you need to replicate entire multi-service environments across accounts/regions, track infrastructure changes in Git, detect configuration drift, or manage non-application resources (like IAM policies, VPCs, or serverless architectures)

---

#### AWS CodeDeploy

AWS CodeDeploy is a managed deployment service that automates application releases to Amazon EC2 instances, on-premises servers, AWS Lambda functions, and Amazon ECS services. It pulls code and artifacts from Amazon S3, GitHub, or Bitbucket, supports automatic rollbacks, and works without requiring changes to your existing application code.

- You can deploy a nearly unlimited variety of application content, including: Code, Serverless AWS Lambda functions, Web and configuration files, Executables, Packages, Scripts, Multimedia files
- CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function. You do not need to make changes to your existing code before you can use CodeDeploy.
- CodeDeploy makes it easier for you to:
  - Rapidly release new features
  - Update AWS Lambda function versions
  - Avoid downtime during application deployment
  - Handle the complexity of updating your applications, without many of the risks associated with error-prone manual deployments.
- The service scales with your infrastructure so you can easily deploy to one instance or thousands.

- **Some key concepts of CodeDeploy** :
  - Application : The unique name or container identifying the software you want to deploy.
  - Revision : A specific version of your application code, configuration files, or Lambda definition paired with an AppSpec file (appspec.yml or appspec.json).
  - Deployment Group : The target set of EC2 instances, on-premises servers, Lambda functions, or ECS services, along with deployment rules, triggers, and rollback settings.
  - Deployment Configuration : Rules that control rollout pace and health thresholds (such as one-at-a-time, half-at-a-time, or all-at-once on EC2/on-premises, or canary/linear traffic shifting on Lambda and ECS).
  - AppSpec File & Lifecycle Hooks : A manifest defining file destinations and scripts that run at specific stages (such as BeforeInstall, AfterInstall, ApplicationStart, and ValidateService).

- **Benefits of AWS CodeDeploy** : CodeDeploy offers these benefits :-
  - _Server, serverless, and container applications_ : CodeDeploy lets you deploy both traditional applications on servers and applications that deploy a serverless AWS Lambda function version or an Amazon ECS application.
  - _Automated deployments_ : CodeDeploy fully automates your application deployments across your development, test, and production environments. CodeDeploy scales with your infrastructure so that you can deploy to one instance or thousands.
  - _Minimize downtime_ : If your application uses the EC2/On-Premises compute platform, CodeDeploy helps maximize your application availability.
    - During an in-place deployment, CodeDeploy performs a rolling update across Amazon EC2 instances. You can specify the number of instances to be taken offline at a time for updates.
    - During a blue/green deployment, the latest application revision is installed on replacement instances. Traffic is rerouted to these instances when you choose, either immediately or as soon as you are done testing the new environment. For both deployment types, CodeDeploy tracks application health according to rules you configure.
  - _Stop and roll back_ : You can automatically or manually stop and roll back deployments if there are errors.
  - _Centralized control_ : You can launch and track the status of your deployments through the CodeDeploy console or the AWS CLI. You receive a report that lists when each application revision was deployed and to which Amazon EC2 instances.
  - _Easy to adopt_ : CodeDeploy is platform-agnostic and works with any application. You can easily reuse your setup code. CodeDeploy can also integrate with your software release process or continuous delivery toolchain.
  - _Concurrent deployments_ : If you have more than one application that uses the EC2/On-Premises compute platform, CodeDeploy can deploy them concurrently to the same set of instances.

- **Overview of CodeDeploy compute platforms** : CodeDeploy is able to deploy applications to three compute platforms:
  i. _EC2/On-Premises_ : Describes instances of physical servers that can be Amazon EC2 cloud instances, on-premises servers, or both. Applications created using the EC2/On-Premises compute platform can be composed of executable files, configuration files, images, and more. Deployments that use the EC2/On-Premises compute platform manage the way in which traffic is directed to instances by using an in-place or blue/green deployment type.
  ii. _AWS Lambda_ : Used to deploy applications that consist of an updated version of a Lambda function. AWS Lambda manages the Lambda function in a serverless compute environment made up of a high-availability compute structure. All administration of the compute resources is performed by AWS Lambda.
  iii. _Amazon ECS_ : Used to deploy an Amazon ECS containerized application as a task set. CodeDeploy performs a blue/green deployment by installing an updated version of the application as a new replacement task set. CodeDeploy reroutes production traffic from the original application task set to the replacement task set. The original task set is terminated after a successful deployment.

- **Overview of CodeDeploy deployment types** : CodeDeploy provides two deployment type options:
  - _In-place deployment_ : The application on each instance in the deployment group is stopped, the latest application revision is installed, and the new version of the application is started and validated. You can use a load balancer so that each instance is deregistered during its deployment and then restored to service after the deployment is complete. Only deployments that use the EC2/On-Premises compute platform can use in-place deployments.
  - _Blue/green deployment_ : The behavior of your deployment depends on which compute platform you use:
    - **Blue/green on an EC2/On-Premises compute platform** : The instances in a deployment group (the original environment) are replaced by a different set of instances (the replacement environment) using these steps :-
      - Instances are provisioned for the replacement environment.
      - The latest application revision is installed on the replacement instances.
      - An optional wait time occurs for activities such as application testing and system verification.
      - Instances in the replacement environment are registered with one or more Elastic Load Balancing load balancers, causing traffic to be rerouted to them. Instances in the original environment are deregistered and can be terminated or kept running for other uses.
    - **Blue/green on an AWS Lambda or Amazon ECS compute platform** : Traffic is shifted in increments according to a canary, linear, or all-at-once deployment configuration.
    - **Blue/green deployments through CloudFormation** : Traffic is shifted from your current resources to your updated resources as part of an CloudFormation stack update. Currently, only ECS blue/green deployments are supported.

#### AWS CodeCommit :

CodeCommit is a secure, highly scalable, managed source control service that hosts private Git repositories. CodeCommit eliminates the need for you to manage your own source control system or worry about scaling its infrastructure. You can use CodeCommit to store anything from code to binaries. It supports the standard functionality of Git, so it works seamlessly with your existing Git-based tools.

- With CodeCommit, you can :
  - _Benefit from a fully managed service hosted by AWS_ : CodeCommit provides high service availability and durability and eliminates the administrative overhead of managing your own hardware and software. There is no hardware to provision and scale and no server software to install, configure, and update.
  - _Store your code securely_ : CodeCommit repositories are encrypted at rest as well as in transit.
  - _Work collaboratively on code_ : CodeCommit repositories support pull requests, where users can review and comment on each other's code changes before merging them to branches; notifications that automatically send emails to users about pull requests and comments; and more.
  - _Easily scale your version control projects_ : CodeCommit repositories can scale up to meet your development needs. The service can handle repositories with large numbers of files or branches, large file sizes, and lengthy revision histories.
  - _Store anything, anytime_ : CodeCommit has no limit on the size of your repositories or on the file types you can store.
  - _Integrate with other AWS and third-party services_ : CodeCommit keeps your repositories close to your other production resources in the AWS Cloud, which helps increase the speed and frequency of your development lifecycle. It is integrated with IAM and can be used with other AWS services and in parallel with other repositories.
  - Easily migrate files from other remote repositories. You can migrate to CodeCommit from any Git-based repository.
  - Use the Git tools you already know. CodeCommit supports Git commands as well as its own AWS CLI commands and APIs.

- **How does CodeCommit work?** : CodeCommit is familiar to users of Git-based repositories, but even those unfamiliar should find the transition to CodeCommit relatively simple. CodeCommit provides a console for the easy creation of repositories and the listing of existing repositories and branches. In a few simple steps, users can find information about a repository and clone it to their computer, creating a local repo where they can make changes and then push them to the CodeCommit repository. Users can work from the command line on their local machines or use a GUI-based editor.

#### AWS CodeBuild :

- AWS CodeBuild is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your own build servers.
- It provides prepackaged build environments for popular programming languages and build tools such as Apache Maven, Gradle, and more. You can also customize build environments in CodeBuild to use your own build tools. CodeBuild scales automatically to meet peak build requests. CodeBuild provides these benefits :
  - Fully managed – CodeBuild eliminates the need to set up, patch, update, and manage your own build servers.
  - On demand – CodeBuild scales on demand to meet your build needs. You pay only for the number of build minutes you consume.
  - Out of the box – CodeBuild provides preconfigured build environments for the most popular programming languages. All you need to do is point to your build script to start your first build.
- You can use the AWS CodeBuild or AWS CodePipeline console to run CodeBuild. You can also automate the running of CodeBuild by using the AWS Command Line Interface (AWS CLI) or the AWS SDKs.

#### AWS CodePipeline :

AWS CodePipeline is a managed continuous integration and continuous delivery (CI/CD) service that automates software build, test, and deployment workflows whenever code changes. It orchestrates AWS services and third-party tools across defined pipeline stages.

#### AWS CodeArtifact :

AWS CodeArtifact is a fully managed artifact repository service used to securely store, publish, and share software packages and dependencies across development teams and CI/CD pipelines. It works with build tools and package managers such as Maven, Gradle, npm, yarn, pip, twine, and NuGet.

- Some Key Concepts & Features :
  - Domains : Top-level containers that group multiple repositories, share package storage across them, and enforce centralized access policies.
  - Repositories : Store package versions and connect to upstream repositories or public registries (like npmjs or Maven Central) to cache external dependencies and protect builds against public outages.
  - Security & Networking : Integrates with AWS IAM for access control, AWS KMS for encryption, and AWS PrivateLink for private access within a VPC without traversing the public internet.
  - CI/CD Integration : Connects with tools like AWS CodeBuild and CodePipeline to pull dependencies and publish internal build artifacts.

#### AWS Systems Manager :

AWS Systems Manager is a centralized operations and management service for viewing, controlling, and automating infrastructure across AWS, on-premises, and multicloud environments. It uses the open-source SSM Agent and IAM permissions to manage nodes without opening inbound SSH/RDP ports or maintaining bastion hosts.

- Key Capabilities :
  - _Node Management_ : Use Fleet Manager to view and manage Linux, Windows, and hybrid nodes, Session Manager for browser/CLI terminal access without key pairs, and Run Command for remote ad-hoc execution.
  - _Configuration & Patching_ : Enforce desired configurations with State Manager, scan and install OS/application updates with Patch Manager, and schedule execution windows with Maintenance Windows.
  - _Automation & Change Control_ : Run multi-step workflows (runbooks) across AWS, Azure, and Google Cloud via Automation, and manage approval workflows through Change Manager.
  - _Visibility & Parameters_ : Track resource health and compliance across accounts using Explorer, Inventory, and Compliance, and store configuration data or secrets in Parameter Store (integrated with AWS KMS). (Note: Application Manager is no longer available to new customers.)

- You can run Systems Manager with setup,
  - SSM Agent : Installed and running on target nodes (pre-installed on many Linux/Windows AMIs).
  - IAM Permissions : An instance profile/role (such as AmazonSSMManagedInstanceCore) allowing communication over HTTPS (port 443) via ssm, ec2messages, and ssmmessages endpoints
