# Amazon Web Services (AWS)

Amazon Web Services offers a broad set of global cloud-based products including compute, storage, databases, analytics, networking, mobile, developer tools, management tools, IoT, security, and enterprise applications: on-demand, available in seconds, with pay-as-you-go pricing. From data warehousing to deployment tools, directories to content delivery, over 200 AWS services are available.

---

### AWS Global Infrastructure

The AWS Cloud infrastructure is built around AWS Regions and Availability Zones. The AWS Global Infrastructure spans 39 Geographic Regions and 124 Availability Zones worldwide, connected by nearly 20 million kilometers of fiber optic cabling. It relies on isolated regions, multi-AZ fault tolerance, and edge locations to deliver low-latency cloud and edge services. Below are mentioned some of the core building blocks :

- **AWS Regions** : These are independent geographic areas containing multiple data centers designed for data sovereignty and compliance.
- **AWS Availability Zones** : An availability zone (AZ) is an isolated location inside a cloud provider's region consisting of one or more physical data centers. It has distinct facilities within a region with independent power, cooling, and security, linked by low-latency networks. Each region has multiple availability zones (usually 3, min is 3, max is 6).
  - Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity. They’re separate from each other, so that they’re isolated from disasters. They’re connected with high bandwidth, ultra-low latency networking.
  - Fault Isolation : Each zone acts as a distinct failure domain so that power outages, network issues, or physical events affect only that specific zone.
  - Low Latency : Zones within the same region connect via high-speed, private, low-latency network links.
  - Redundancy : Cloud providers (such as Amazon Elastic Compute Cloud and Microsoft Azure) require multiple AZs per region to let applications replicate data and auto-scale safely.
  - Structure : A single zone can house up to five physical data centers, but no two availability zones ever share the exact same physical building or infrastructure
- **AWS Regional Services** : Each region has a specific set of services it can offer.
- **Points of Presence (PoPs)** : A global network of edge locations and regional edge caches for content delivery. Amazon has 400+ Points of Presence (400+ Edge Locations & 10+ Regional Caches) in 90+ cities across 40+ countries. Content is delivered to end users with lower latency.

- **How to choose an AWS Region?**
  - Compliance with data governance and legal requirements : data never leaves a region without your explicit permission
  - Proximity to customers : reduced latency
  - Available services within a Region : new services and new features aren’t available in every Region.
  - Pricing : pricing varies region to region and is transparent in the service pricing page.

### _**AWS Shared Responsibility Model**_

![awsSharedResponsibilityMOodel](https://d1.awsstatic.com/onedam/marketing-channels/website/aws/en_US/product-categories/security-identity-compliance/compliance/approved/images/7a404923-5572-409c-b30e-6d44706bcd89.92c57224d8acd09bf44d94bc25db5c58419a8941.jpeg)

AWS Shared Responsibility Model divides cloud security and compliance duties between Amazon Web Services (AWS) and the customer. It is summarized by the principle : AWS is responsible for security _**of the cloud**_, and customers are responsible for security _**in the cloud**_.

- Security and Compliance is a shared responsibility between AWS and the customer. This shared model can help relieve the customer’s operational burden as AWS operates, manages and controls the components from the host operating system and virtualization layer down to the physical security of the facilities in which the service operates.
- The customer assumes responsibility and management of the guest operating system (including updates and security patches), other associated application software as well as the configuration of the AWS provided security group firewall. Customers should carefully consider the services they choose as their responsibilities vary depending on the services used, the integration of those services into their IT environment, and applicable laws and regulations.
- The nature of this shared responsibility also provides the flexibility and customer control that permits the deployment. As shown in the chart below, this differentiation of responsibility is commonly referred to as Security “of” the Cloud versus Security “in” the Cloud.

1. <ins>**AWS Responsibility: "Security of the Cloud"**</ins> : AWS manages, protects, and controls the underlying infrastructure that runs all services offered in the AWS Cloud. This includes:

- Physical Security: Data centers, hardware, surveillance, and environmental controls.
- Global Infrastructure: Regions, Availability Zones, and edge locations.
- Hardware & Compute: Servers, storage hardware, and networking gear.
- Virtualization Layer: The hypervisor and host operating systems.

2. <ins>**Customer Responsibility: "Security in the Cloud"**</ins> : The customer's exact obligations depend on the specific AWS service model they choose (IaaS, PaaS, or SaaS). General customer duties include:

- Customer Data: Classifying, backing up, and protecting content and data.
- Identity and Access Management (IAM): Managing user accounts, permissions, roles, and Multi-Factor Authentication (MFA).
- Network & Firewall Configuration: Configuring security groups, Network Access Control Lists (NACLs), and virtual private clouds (VPCs).
- Operating System & Applications: Patching, updating, and securing guest operating systems and application software (especially in IaaS models like Amazon EC2)

3. <ins>**Shared Controls & Shifting Responsibilities**</ins> : Some controls apply to both parties in different contexts:

- Patch Management : AWS patches and fixes flaws in the underlying infrastructure; the customer patches their guest operating systems and application code.
- Configuration Management : AWS provides secure configuration tools and default baselines, while customers must properly configure their resources.
- Awareness & Training : AWS trains its internal staff; customers are responsible for training their own personnel.
- Infrastructure-as-a-Service (EC2) : You manage the guest OS, patches, firewall rules, and application stack.
- Platform-as-a-Service (RDS) : AWS handles the database engine patching and OS updates, while you manage database access controls, queries, and data encryption.
- Serverless (Lambda) : AWS manages the servers, OS, and runtime environment, while you are responsible for your function code, IAM roles, and input validation.
