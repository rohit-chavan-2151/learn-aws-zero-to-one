### Amazon Elastic Container Service (ECS)

Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications.

- As a fully managed service, Amazon ECS comes with AWS configuration and operational best practices built-in. It's integrated with both AWS tools, such as Amazon Elastic Container Registry, and third-party tools, such as Docker.
- This integration makes it easier for teams to focus on building the applications, not the environment. You can run and scale your container workloads across AWS Regions in the cloud, and on-premises, without the complexity of managing a control plane.

- **Terminology and components** : There are three layers in Amazon ECS:
  i. _Capacity_ - The infrastructure where your containers run
  ii. _Controller_ - Deploy and manage your applications that run on the containers
  iii. _Provisioning_ - The tools that you can use to interface with the scheduler to deploy and manage your applications and containers

The following diagram shows the Amazon ECS layers :

![ComponentsOfECS](https://docs.aws.amazon.com/images/AmazonECS/latest/developerguide/images/ecs-layers.png)

- The capacity is the infrastructure where your containers run. The following is an overview of the capacity options:
  - Amazon ECS Managed Instances is a compute option for Amazon ECS that enables you to run containerized workloads on a range of Amazon EC2 instance types while offloading infrastructure management to AWS. With Amazon ECS Managed Instances, you can access specific compute capabilities such as GPU acceleration, specific CPU architectures, high network performance, and specialized instances types, while AWS handles provisioning, patching, scaling, and maintenance of the underlying infrastructure.
  - Amazon EC2 instances in the AWS cloud : You choose the instance type, the number of instances, and manage the capacity.
  - Serverless in the AWS cloud : Fargate is a serverless, pay-as-you-go compute engine. With Fargate you don't need to manage servers, handle capacity planning, or isolate container workloads for security.
  - On-premises virtual machines (VM) or servers : Amazon ECS Anywhere provides support for registering an external instance such as an on-premises server or virtual machine (VM), to your Amazon ECS cluster.
  - The Amazon ECS scheduler is the software that manages your applications.

- **Features of ECS** : Amazon ECS provides the following high-level features:
  - _Task definition_ : The blueprint for the application.
  - _Cluster_ : The infrastructure your application runs on.
  - _Task_ : An application such as a batch job that performs work, and then stops.
  - _Service_ : A long running stateless application.
  - _Account Setting_ : Allows access to features.
  - _Cluster Auto Scaling_ : Amazon ECS manages the scaling of Amazon EC2 instances that are registered to your cluster.
  - _Service Auto Scaling_ : Amazon ECS increases or decreases the desired number of tasks in your service automatically.

---

### AWS Fargate

AWS Fargate is a serverless, pay-as-you-go compute engine for running containers with Amazon ECS and Amazon EKS. It removes the need to provision, configure, or manage virtual machines or EC2 clusters.

- Fargate is a technology that provides on-demand, right-sized compute capacity for containers. With Fargate, you don’t have to provision, configure, or scale groups of virtual machines on your own to run containers. You also don’t need to choose server types, decide when to scale your node groups, or optimize cluster packing.
  - You can control which Pods start on Fargate and how they run with Fargate profiles. Fargate profiles are defined as part of your Amazon EKS cluster. Amazon EKS integrates Kubernetes with Fargate by using controllers that are built by AWS using the upstream, extensible model provided by Kubernetes.
  - These controllers run as part of the Amazon EKS managed Kubernetes control plane and are responsible for scheduling native Kubernetes Pods onto Fargate. The Fargate controllers include a new scheduler that runs alongside the default Kubernetes scheduler in addition to several mutating and validating admission controllers.
  - When you start a Pod that meets the criteria for running on Fargate, the Fargate controllers that are running in the cluster recognize, update, and schedule the Pod onto Fargate.
- With Fargate, you only pay for the resources your containers use (CPU and memory), and AWS automatically provisions the appropriate infrastructure for you. This makes AWS Fargate a cost-effective and efficient solution for developers and businesses looking to simplify container management.

- **What is Serverless** : Serverless computing is a cloud computing model that allows developers to run code or applications without provisioning or managing the underlying servers. Serverless computing abstracts away the infrastructure so developers can focus on writing code and building applications, instead of worrying about managing servers.
  - AWS Fargate represents the serverless concept for containers. Unlike traditional container services where you must manage EC2 instances and clusters, Fargate automatically allocates the compute resources required for your containers to run. It allows you to define your application’s resource needs (e.g., CPU, memory), and then it handles the rest.
  - The game-changing aspect of AWS Fargate is that it completely removes the need for managing infrastructure. Developers can now focus on building scalable applications without the complexity of server management, which significantly reduces both operational overhead and costs.

  ![AWSFargate](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRVfcqE4nQCJdHLHwOvD23fH43VE9ysQ5YDZanBQ8o5ag&s=10)

- **Features of AWS Fargate** : AWS Fargate comes with several powerful features that make it a top choice for containerized application management:
  - Serverless Container Management : No need to manage servers. AWS Fargate takes care of provisioning and scaling the infrastructure automatically.
  - Pay-as-You-Go Pricing : You only pay for the compute and memory resources used by your containers. This allows for more cost-efficient operations.
  - Seamless Integration with ECS and EKS : Fargate works seamlessly with Amazon ECS and EKS, allowing you to use familiar AWS services for container orchestration.
  - Automatic Scaling : Fargate automatically adjusts your resources based on your application’s needs, scaling up or down depending on traffic or demand.
  - Security and Compliance : AWS Fargate integrates with AWS security services like IAM and VPC to ensure your applications are secure, and your data is protected.

---

### AWS Lambda

AWS Lambda is a serverless, event-driven compute service that runs your code in response to events and automatically manages the underlying compute resources. You upload your code as a "Lambda function," and AWS handles server provisioning, patching, high availability, and scaling

- **How It Works** :
  - Event-driven execution : Code runs only when triggered by an event—such as an HTTP request via Amazon API Gateway, a file upload to Amazon S3, a database update in Amazon DynamoDB, or a message in Amazon SQS.
  - Automatic scaling : Lambda spins up isolated execution environments (powered by Firecracker microVMs) in milliseconds to match incoming traffic—scaling from zero to thousands of parallel executions without configuration.
  - Pay-as-you-go pricing : You pay only for the number of requests ($0.20 per million) and the duration your code executes (measured in milliseconds and allocated memory), with zero charges when your code is idle

- **The Event-Driven Model** : Every Lambda execution follows a three-part pattern,
  - An event occurs, such as a file uploaded to S3, an HTTP request hitting API Gateway, or a message arriving in an SQS queue.
  - AWS spins up your code to process that specific event.
  - The function performs an action, such as saving data to DynamoDB, returning an HTTP response, or writing a processed file back to S3.

- **Key Specifications & Limits** :
  - Supported languages : Native runtimes include Node.js, Python, Java, Go, .NET (C#), and Ruby, plus support for custom runtimes and container images.
  - Execution limits : Functions can allocate between 128 MB and 10,240 MB of memory and run for a maximum timeout of 15 minutes (900 seconds) per invocation.
  - Cold starts : When a function scales up after being idle, initializing a new microVM causes a brief latency delay known as a "cold start". Features like Provisioned Concurrency and Lambda SnapStart keep environments pre-initialized to eliminate this delay.

---
