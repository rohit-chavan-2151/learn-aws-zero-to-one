# AWS Cloud Computing

---

### What is Cloud Computing?

Cloud computing is an internet-based computing service in which large groups of remotes servers are networked to allow
centralized data storage, and online access to computer services or resources.
So basically, it is known as 'On-demand' delivery of IT resources over the internet with pay-as-you-go pricing. Using cloud computing, organizations can use shared computing and storage resources rather than building, operating, and improving infrastructure on their own.
Cloud computing is a model that enables the following features.

- Users can provision and release resources on-demand.
- Resources can be scaled up or down automatically, depending on the load.
- Resources are accessible over a network with proper security.
- Cloud service providers can enable a pay-as-you-go model, where customers are charged based on the type of resources and per usage.

#### _Some of the Characteristics_

All cloud services share the fundamental characteristics that define them :-

- **On-demand self-services** : The Cloud computing services does not require any human administrators, user themselves are able to provision, monitor and manage computing resources as needed.
- **Broad network access** : The Computing services are generally provided over standard networks and heterogeneous devices.
- **Rapid elasticity** : The Computing services should have IT resources that are able to scale out and in quickly and on a need basis. Whenever the user require services it is provided to him and it is scale out as soon as its requirement gets over.
- **Resource pooling** : The IT resource (e.g., networks, servers, storage, applications, and services) present are shared across multiple applications and occupant in an uncommitted manner. Multiple clients are provided service from a same physical resource.
- **Measured service** : The resource utilization is tracked for each application and occupant, it will provide both the user and the resource provider with an account of what has been used. This is done for various reasons like monitoring billing and effective use of resource.
- **Multi-tenancy** : Cloud computing providers can support multiple tenants (users or organizations) on a single set of shared resources.
- **Virtualization** : Cloud computing providers use virtualization technology to abstract underlying hardware resources and present them as logical resources to users.
- **Resilient computing** : Cloud computing services are typically designed with redundancy and fault tolerance in mind, which ensures high availability and reliability.
- **Flexible pricing models** : Cloud providers offer a variety of pricing models, including pay-per-use, subscription-based, and spot pricing, allowing users to choose the option that best suits their needs.
- **Security** : Cloud providers invest heavily in security measures to protect their users' data and ensure the privacy of sensitive information.
- **Automation** : Cloud computing services are often highly automated, allowing users to deploy and manage resources with minimal manual intervention.
- **Sustainability** : Cloud providers are increasingly focused on sustainable practices, such as energy-efficient data centers and the use of renewable energy sources, to reduce their environmental impact.

#### _**The 7 Core Advantages of Cloud Computing**_ :

1. **On-Demand Scalability** : Maintaining traditional IT infrastructure during economic downturns, rapid expansions, or supply chain disruptions is incredibly difficult. The cloud provides the ability to scale horizontally or vertically at your own speed. Whether you need to aggressively provision resources for a new launch or downscale during a quiet season, you only pay for what you use.

2. **Enhanced Security** : Small businesses are heavily targeted by cyberattacks, yet many lack the resources to maintain an in-house cybersecurity team. Migrating to the cloud provides immediate access to industry-standard data encryption, enterprise firewalls, and 24/7 automated network monitoring that would otherwise be cost-prohibitive.

3. **Access to Modern Technology** : The cloud is much more than storage; it is an innovation engine. Businesses can leverage cloud environments to access cutting-edge technologies without buying physical servers. This includes tapping into robust computational power for Artificial Intelligence, Machine Learning models, Big Data Analytics, and containerization.

4. **Cost-Effectiveness** : Based on the 'pay-as-you-go' utility model, the cloud eliminates the CapEx (Capital Expenditure) of buying servers, hard drives, and networking gear. Instead, it shifts IT spending to a manageable OpEx (Operational Expenditure) model, removing the need to house, cool, and maintain physical data centers.

5. **Enterprise Mobility** : The cloud untethers the workforce from the physical office. Employees can securely compute heavy tasks, access critical workflows, and manage data from anywhere in the world, fostering a better work-life balance and enabling remote work models.

6. **Seamless Collaboration** : Cloud services eradicate version-control nightmares. By keeping data in a centralized, cloud-hosted environment, multiple departments, clients, and partners can collaborate simultaneously on the same document or application. This creates a "single source of truth," reducing errors and duplication.

7. **Advanced Predictive Analytics** : Cloud computing democratizes big data. Businesses can rent massive processing capacities on-demand to run complex predictive analytics. By analyzing historical data, companies can predict market trends, automate low-value processes, and optimize their business strategies based on deep customer insights.

### _**Architecture of Cloud Computing**_

Cloud computing architecture is the blueprint of components and subcomponents—including a front-end platform, back-end infrastructure, a network, and a cloud-based delivery model—that work together to deliver on-demand computing.

_Core components of Cloud Architecture_ :

- **The Frontend (Client Side)** : It contains all the user interfaces and client infrastructure required for end-users to interact with the cloud. This is the visible interface through which users interact directly with the cloud environment. It acts as the gateway, allowing users to seamlessly access cloud-based services without understanding the underlying infrastructure.
  - Client Infrastructure : The client infrastructure refers to the hardware and software components used by the end-user to access cloud services. It forms the frontend of cloud architecture and provides the interface through which users interact with cloud applications.
  - Hardware : Devices such as laptops, desktop computers, smartphones, and tablets.
  - Software : Web browsers, mobile applications, and other client-side software used to access cloud services.
  - User Interface : Provides a Graphical User Interface (GUI) through which users can interact with cloud applications.
  - Communication : Sends user requests to the cloud through the Internet and receives the required data or results.
  - Access : Allows users to access cloud services from different devices and locations.

- **The Backend (Cloud Provider Side)** : This is the "cloud" itself. It consists of all the resources required to provide cloud computing services. It comprises of huge data storage, virtual machines, security mechanism, services, deployment models, servers etc.
  - _Application_ : It can be software or platforms that process client requests and deliver the necessary outcomes to end-users. The specific application selected depends heavily on client requirements and resource availability.
  - _Service Delivery_ : Provides the required services or results to end-users.
  - _Resource Utilization_ : Uses available cloud resources such as computing power, storage, and databases.
  - _User Requirements_ : Applications are selected or designed based on the specific needs of the client.
  - _Services_ : It manages each and every operations that runs on the cloud computing platform. It manages the different types of services that users can access based on their specific requirements.

**Runtime Cloud** : It provides virtual machines an environment for executing and running programs at the same time. In other words, it performs similarly to a cloud-based operating system software that uses virtualization technologies to execute services, enabling multiple run times on the same server.

In other words : A physical server can host multiple virtual machines. Each virtual machine can have its own runtime environment. Different applications can run simultaneously without interfering with one another. The runtime provides the necessary environment for applications to execute properly. This allows cloud providers to use physical servers efficiently.

**Storage** : It is one of the most important components of cloud computing. These services are used to store and manage data. Several users can access the data simultaneously within the cloud storage system. Popular cloud storage solutions include:

- Amazon S3 is a scalable object storage service
- Microsoft Azure Storage includes blob storage, table storage, and file shares
- Google Cloud Storage offers high-performance and durable storage for various workloads

**Infrastructure** : It provides services on three levels: Host, Network, and Application.

- Host level provides computing resources required to run cloud services.
- Network level provides communication between cloud resources and users.
- Application level provides the actual software and services used by users.

**Management** : It allocates specific resources for tasks and coordinates multiple functions simultaneously within the cloud environment. It ensures that by:

- Monitoring the performance and availability of cloud resources.
- Allocating and managing computing, storage, and networking resources.
- It helps increase or decrease resources according to workload.
- It handles activities such as configuration, maintenance, resource utilization, and billing.

**Security** : It protects cloud resources, applications, services, infrastructure, and data from unauthorized access and security threats. The security layer ensures:

- Secure authentication & identity management (e.g., AWS IAM, Azure Active Directory)
- Data encryption for sensitive information
- Firewall protection & threat detection to mitigate cyberattacks
- Disaster recovery & backup mechanisms for data resilience

**Internet** : The Internet acts as a communication medium or bridge between the frontend and backend of a cloud computing architecture. It allows users to connect to cloud services and enables data and requests to travel between the user's device and the cloud servers.

![CloudArchitecture](https://www.infosectrain.com/wp-content/uploads/2023/07/architecture-of-cloud-computing-.jpg)

### Types of Cloud :-

1. _**Infrastructure as a Service ( IaaS )**_ : It is a type of cloud computing that gives people access to IT tools like virtual computers, storage, and networks through the internet. You don’t need to buy or manage physical hardware. Instead, you pay only for what you use.

Example: Amazon EC2 is an Infrastructure as a Service (IaaS) that provides virtual servers on the cloud, allowing users to create, manage, and scale computing resources as needed.

Benefits of using IaaS ->

- **Flexibility and Control** : It comes up with providing virtualized computing resources such as VMs, Storage, and networks facilitating users with control over the Operating system and applications.
- **Reducing Expenses of Hardware** : It provides business cost savings with the elimination of physical infrastructure investments making it cost-effective.
- **Scalability of Resources** : The cloud provides in scaling of hardware resources up or down as per demand facilitating optimal performance with cost efficiency.

2. _**Platform as a Service ( PaaS )**_ : It is a cloud computing model where a third-party provider offers the software and hardware tools needed to develop, test, and run applications. This allows users to focus on building their applications without worrying about managing servers or infrastructure.

Example: AWS Elastic Beanstalk is a Platform as a Service (PaaS) by Amazon Web Services that helps developers deploy and manage applications easily while AWS handles servers, scaling, and load balancing.

Benefits of using PaaS ->

- **Simplifying the Development** : It offers application development by keeping the underlying Infrastructure as an Abstraction. It helps the developers to completely focus on application logic ( Code ) and background operations are completely managed by the AWS platform.
- **Enhancing Efficiency and Productivity** : It lowers the Management of Infrastructure complexity, speeding up the Execution time and bringing the updates quickly to market by streamlining the development process.
- **Automation of Scaling** : Management of resource scaling, guaranteeing the program's workload efficiency is ensured by PaaS.

3. _**Software as a Service (SaaS)**_ : It is a way of using software over the internet instead of installing it on your computer. The software is hosted by a company, and you can use it just by logging in through a web browser. You don’t need to worry about updates, maintenance, or storage the provider takes care of all that.

Example: Google Docs allows users to create, edit, and share documents online without installing any software.

Benefits of using SaaS ->

- **Collaboration And Accessibility** : It helps users to easily access applications without having the requirement of local installations. It is fully managed by the AWS Software working as a service over the internet encouraging effortless cooperation and ease of access.
- **Automation of Updates** : It providers manage the handling of software maintenance with automatic latest updates ensuring users gain experience with the latest features and security patches.
- **Cost Efficiency** : It acts as a cost-effective solution by reducing the overhead of IT support by eliminating the need for individual software licenses.

4. _**Function as a Service (FaaS)**_ : It is a cloud-computing service that allows customers to run code in response to events, without managing the complex infrastructure. You just write the code, upload it and the cloud provider runs it only when it's needed. You pay only for the time your code runs.

Example: AWS Lambda lets you run code automatically when an event occurs, such as uploading a photo to a website, without managing or running servers all the time.

Benefits of using FaaS ->

- **Event-Driven Execution** : It helps in the maintenance of servers and infrastructure making users worry about it. FaaS facilitates the developers to run code as a response to the events.
- **Cost Efficiency** : FaaS facilitates cost efficiency by coming up with the principle "Pay as per you Run" for the computing resources used.
- **Scalability and Agility** : Serverless Architectures scale effortlessly in handing the workloads promoting agility in development and deployment.

### _Cloud Deployment Models_:-

A cloud deployment model defines where your cloud infrastructure lives, who owns and manages it, and how it is accessed. It establishes the boundaries of your cloud environment, dictating what you can customize, how resources are shared among users, and the overarching purpose of the setup.

Understanding these models is the crucial first step for any business migrating to the cloud, as each offers distinct trade-offs in governance, cost, security, and management.

There are three types of clouds - Public, Private, and Hybrid cloud.

1. **Public Cloud** : The public cloud delivers infrastructure and services over the internet to the general public or broad industry groups. The infrastructure is entirely owned, managed, and maintained by a third-party cloud service provider (e.g., Google Cloud, AWS, Microsoft Azure). Resources are shared among multiple tenants.

   ![PublicCloud](https://media.geeksforgeeks.org/wp-content/uploads/20211123123729/Group4-660x330.jpg)

_Advantages of the Public Cloud Model_ :

- Minimal Investment : Operates on a pay-per-use model with no substantial upfront capital expenditure.
- Zero Setup & Maintenance: The provider subsidizes and manages all physical hardware setup and ongoing maintenance.
- Dynamic Scalability : On-demand resources are nearly limitless, scaling instantly to fulfill business needs.

_Disadvantages of the Public Cloud Model_ :

- Lower Security : Because resources are shared publicly, meeting strict, high-level compliance and security standards can be challenging.
- Low Customization : The standardized environment offers little room for bespoke hardware or infrastructure customizations.

2. **Private Cloud** : The private cloud deployment model is the exact opposite of the public cloud deployment model. It's a one-on-one environment for a single user (customer). There is no need to share your hardware with anyone else. The distinction between private and public clouds is in how you handle all of the hardware. It is also called the "internal cloud" & it refers to the ability to access systems and services within a given border or organization. The cloud platform is implemented in a cloud-based secure environment that is protected by powerful firewalls and under the supervision of an organization's IT department. The private cloud gives greater flexibility of control over cloud resources.

   ![PrivateCloud](https://media.geeksforgeeks.org/wp-content/uploads/20211123123851/Group1-660x330.jpg)

_Advantages of the Private Cloud Model_ :

- Total Control : You have complete command over IT operations, service integration, and user behavior.
- Elite Security and Privacy : Ideal for sensitive corporate data, allowing for strict access controls and physical isolation.
- Legacy System Support : Highly customizable, making it capable of supporting legacy applications that cannot migrate to a public environment.

_Disadvantages of the Private Cloud Model_ :

- High Cost : Personalized facilities, dedicated hardware, and internal IT management make this the most expensive option.
- Limited Scalability : Scaling is restricted by the physical capacity of the dedicated hardware purchased

3. **Hybrid Cloud** : By bridging the public and private worlds with a layer of proprietary software, hybrid cloud computing gives the best of both worlds. With a hybrid solution, you may host the app in a safe environment while taking advantage of the public cloud's cost savings. Organizations can move data and applications between different clouds using a combination of two or more cloud deployment methods, depending on their needs.

   ![HybridCloud](https://media.geeksforgeeks.org/wp-content/uploads/20211123123930/Group2-660x330.jpg)

_Advantages of the Hybrid Cloud Model_ :

- Ultimate Flexibility : Businesses can keep sensitive data secure on the private cloud while running heavy, non-sensitive applications on the public cloud.
- Cost Efficiency : You only pay for additional public cloud capacity when you experience traffic spikes that your private cloud cannot handle (known as "cloud bursting").
- Targeted Security : Data theft risks are reduced by keeping the most critical assets completely isolated.

_Disadvantages of the Hybrid Cloud Model_ :

- Difficult to manage : Hybrid clouds are difficult to manage as it is a combination of both public and private cloud. So, it is complex.
- Slow data transmission : Data transmission in the hybrid cloud takes place through the public cloud so latency occurs.

4. **Multi Cloud** : While a hybrid cloud mixes private and public models, a multi-cloud strategy specifically involves using multiple public cloud providers at the same time (e.g., using AWS for storage, Google Cloud for machine learning, and Azure for active directory).

   ![MultiCloud](https://media.geeksforgeeks.org/wp-content/uploads/20260302182448351287/multi_cloud_vs_hybrid_cloud.webp)

_Advantages of the Multi-Cloud Model_ :

- Best-of-Breed Features : You can mix and match the absolute best tools from different providers to suit specific workloads.
- Reduced Latency : You can route user traffic to the cloud provider that has a data center closest to that specific user.
- High Availability : It is incredibly rare for two different major cloud providers to experience outages simultaneously, creating exceptional disaster recovery.

_Disadvantages of the Multi-Cloud Model_ :

- Complex : The combination of many clouds makes the system complex and bottlenecks may occur.
- Security issue : Due to the complex structure, there may be loopholes to which a hacker can take advantage hence, makes the data insecure.

#### _**How to Choose the Right Deployment Model**_

There is no one-size-fits-all approach. The ideal choice depends entirely on your specific business requirements. Consider these five factors:

- Cost : Determine your budget for upfront capital expenses versus ongoing operational expenses.
- Scalability : Assess your current traffic and predict how rapidly you will need to scale resources in the future.
- Ease of Use : Evaluate the technical expertise of your internal IT staff and their ability to manage complex infrastructures.
- Compliance : Identify any legal or industry regulations (like HIPAA or GDPR) that dictate where and how your data must be stored.
- Privacy : Classify your data to determine what can be public and what requires strict, isolated confidentiality.
