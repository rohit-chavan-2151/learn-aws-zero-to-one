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

#### _Types of Cloud Deployment Models_:-

There are three types of clouds - Public, Private, and Hybrid cloud.

1. **Public Cloud** : In public cloud, the third-party service providers make resources and services available to their customers via Internet. Customer’s data and related security is with the service providers’ owned infrastructure.

2. **Private Cloud** : A private cloud also provides almost similar features as public cloud, but the data and services are managed by the organization or by the third party only for the customer’s organization. In this type of cloud, major control is over the infrastructure so security related issues are minimized.

3. **Hybrid Cloud** : A hybrid cloud is the combination of both private and public cloud. The decision to run on private or public cloud usually depends on various parameters like sensitivity of data and applications, industry certifications and required standards, regulations, etc.
