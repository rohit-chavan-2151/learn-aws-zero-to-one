## <u>AWS Elastic Load Balancing & Auto Scaling Groups</u>

**Scalability** : Scalability refers to a system's ability to handle increasing workloads, users, or data by adding or adjusting resources while maintaining acceptable performance.

- Handling Increased Load : A scalable system can support more users, requests, or data as demand increases.
- Resource Expansion : Resources such as servers, computing power, memory, or storage can be added or adjusted to meet the increased demand.

Different approaches can be used depending on workload, architecture, and infrastructure requirements. These are categorized as : Horizontal scaling and vertical scaling are two approaches to increasing system capacity.

1. **Vertical Scaling** : Vertical scaling, also known as scaling up, increases the resources of an existing machine, such as CPU, memory, or storage. The same server is upgraded instead of adding more servers. More hardware components like RAM or CPU are added to the existing system to increase its capacity for stable performance. It is often simpler to implement because fewer architectural changes are required. It is commonly useful for smaller systems, databases, and applications that do not yet require distributed deployment.

- Advantages :
  - Simple to Implement : Usually requires fewer architectural changes than horizontal scaling.
  - Improved Capacity : More CPU, memory, or storage can increase the workload a machine can handle.
  - Lower Operational Complexity : Fewer machines may be easier to monitor and manage.
- Limitations :
  - Hardware Limits : Scaling is limited by the maximum capacity supported by the machine or platform.
  - Potential Downtime : Some upgrades may require restarting, resizing, or replacing the machine.
  - Limited Failure Isolation : If the workload depends heavily on a single machine, failure of that machine can affect availability unless redundancy is provided.
  - Cost at Higher Tiers : High-capacity machines can become expensive.

2. **Horizontal Scaling** : Horizontal scaling, also known as scaling out, increases system capacity by adding more machines or application instances. These multiple instances share the workload by distributing the traffic to each of the instances. A load balancer is commonly used to distribute incoming traffic. The application and its dependencies must support distributed operation.

- Advantages :
  - Higher Capacity : Additional nodes can process more requests or workloads.
  - Flexible Growth : New instances can be added as demand increases.
  - Improved Availability Potential : Traffic can be redirected to healthy instances when redundancy and failure handling are configured properly.
  - Independent Expansion : Distributed architectures can continue growing beyond the capacity of a single machine.
- Limitations :
  - Higher Complexity : Requires coordination across multiple machines or services.
  - Distributed Data Challenges : Replication, synchronization, and consistency may become more complex.
  - Network Overhead : Communication between distributed nodes introduces additional network dependency and latency.
  - Operational Overhead : Monitoring, deployment, configuration, and orchestration become more complex.

![Scaling](https://media.geeksforgeeks.org/wp-content/uploads/20260416101913435205/vertical_and_horizontal_scaling.webp)

**High Availability** : High availability ensures a system remains operational and accessible with minimal downtime, even when hardware or software components fail.

- Redundancy : Running duplicate or multiple instances of critical components.
- Load Balancing : Routing user requests strictly to healthy nodes while avoiding failed ones.
- Automatic Failover : Detecting crashes and shifting traffic or responsibilities to backup components.
- Multi-AZ / Multi-Region Deployment: Spreading applications across different data centers or geographic regions to survive localized outages.

**Cloud Elasticity** : Cloud elasticity refers to the ability of a cloud environment to dynamically and automatically expand or compress infrastructural resources based on sudden fluctuations in demand.

- Dynamic Adjustment : Automatically provisions extra compute, storage, or network resources (CPU, Memory, Bandwidth) when client access expands, and reduces them when traffic drops.
- Cost Efficiency : Maximizes resource utilization and minimizes infrastructure costs. It is most commonly associated with public cloud pay-per-use models where you only pay for the duration resources are consumed.
- Horizontal Scaling : Typically relies on scale-out arrangements (adding or removing instances dynamically) rather than upgrading existing hardware.
- Best For : Unpredictable workloads or scenarios where resource requirements fluctuate up and down suddenly for specific time intervals. It is not practical for environments requiring a persistent infrastructure for a constant heavy workload.
- Mission-Critical Performance : Ensures that applications maintain performance requirements during sudden spikes, preventing potential business losses due to downtime or latency.

---

### **AWS Elastic Load Balancing (ELB)**

- Elastic Load Balancing is a fully managed service that automatically distributes your incoming application traffic across multiple targets such as Amazon EC2 instances, containers (ECS), Lambda functions, and IP addresses. It helps to manage incoming requests by optimally routing traffic so that no one instance is overwhelmed.
  - By routing traffic across one or more Availability Zones (AZs), ELB prevents any single resource from being overwhelmed, ensuring your applications achieve high availability, fault tolerance, and seamless scalability.
  - It is a managed load balancer, which means AWS guarantees that it will be working, AWS takes care of upgrades, maintenance, high availability, and AWS provides only a few configuration knobs.

- To use Elastic Load Balancing with your Auto Scaling group, attach the load balancer to your Auto Scaling group. This registers the group with the load balancer, which acts as a single point of contact for all incoming web traffic to your Auto Scaling group.
  - When you use Elastic Load Balancing with your Auto Scaling group, it's not necessary to register individual EC2 instances with the load balancer. Instances that are launched by your Auto Scaling group are automatically registered with the load balancer. Likewise, instances that are terminated by your Auto Scaling group are automatically deregistered from the load balancer.
- Elastic Load Balancing creates a network interface for each Availability Zone you enable. Each load balancer node in the Availability Zone uses this network interface to get a static IP address. When you create an Internet-facing load balancer, you can optionally associate one Elastic IP address per subnet.
- You can add Elastic Load Balancing health checks to your Auto Scaling group so that Amazon EC2 Auto Scaling can identify and replace unhealthy instances based on these additional health checks. Otherwise, you can create a CloudWatch alarm that notifies you if the healthy host count of the target group is lower than allowed.

**Core Concepts** :

- Listeners : A listener checks for incoming connection requests on a specific protocol and port.
- Target Groups : A logical group of backend resources such as EC2 instances, containers, IP addresses, or Lambda functions. The load balancer sends traffic to the target group instead of directly to individual instances.
- Health Checks : ELB regularly checks the health of targets using a path like /health. If a target becomes unhealthy, ELB stops routing traffic to it until it recovers.
- Cross-Zone Load Balancing : Distributes traffic evenly across healthy targets in all enabled Availability Zones, helping prevent overload in a single zone.
- Expose a single point of access (DNS) to your application. This means giving your application one primary, human-readable web address (like app.example.com) that points to a central entry point (such as a load balancer, reverse proxy, or API gateway) instead of forcing users or clients to connect directly to individual backend servers or IP addresses.
- Seamlessly handle failures of downstream instances. When a instance or group of instances goes down, the traffic is routed to another instance which is available.

**Types of Load Balancers in AWS** : Elastic Load Balancing provides four types of load balancers that can be used with your Auto Scaling group: _Application Load Balancers_, _Network Load Balancers_, _Gateway Load Balancers_, and _Classic Load Balancers_ (Previous Generation).

There is a key difference in how the load balancer types are configured. With Application Load Balancers, Network Load Balancers, and Gateway Load Balancers, instances are registered as targets with a target group, and you route traffic to the target group. With Classic Load Balancers, instances are registered directly with the load balancer.

![LoadBalancer](https://miro.medium.com/1*2TfBNBKRjPZhbOvTiplGJQ.png)

- <u>**Application Load Balancer**</u> : Routes and load balances at the application layer (HTTP/HTTPS), and supports path-based routing. An Application Load Balancer can route requests to ports on one or more registered targets, such as EC2 instances, in your virtual private cloud (VPC).
  - A load balancer serves as the single point of contact for clients. The load balancer distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones. This increases the availability of your application. You add one or more listeners to your load balancer.
  - A listener checks for connection requests from clients, using the protocol and port that you configure. The rules that you define for a listener determine how the load balancer routes requests to its registered targets. Each rule consists of a priority, one or more actions, and one or more conditions. When the conditions for a rule are met, then its actions are performed. You must define a default rule for each listener, and you can optionally define additional rules.
  - Each target group routes requests to one or more registered targets, such as EC2 instances, using the protocol and port number that you specify. You can register a target with multiple target groups.
  - You can configure health checks on a per target group basis. Health checks are performed on all targets registered to a target group that is specified in a listener rule for your load balancer.
  - The following diagram illustrates the basic components. _Notice that each listener contains a default rule, and one listener contains another rule that routes requests to a different target group. One target is registered with two target groups._

- **Functioning of Application Load Balancer** : An Application Load Balancer functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model.
  - After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action.
  - You can configure listener rules to route requests to different target groups based on the content of the application traffic.
  - Routing is performed independently for each target group, even when a target is registered with multiple target groups. You can configure the routing algorithm used at the target group level.
  - The default routing algorithm is round robin; alternatively, you can specify the least outstanding requests routing algorithm.
  - Elastic Load Balancing scales your load balancer as traffic to your application changes over time. It can scale to the vast majority of workloads automatically.

- <u>**Network Load Balancer**</u> : Routes and load balances at the transport layer (TCP/UDP Layer-4), based on address information extracted from the Layer-4 header. Network Load Balancers can handle traffic bursts, retain the source IP of the client, and use a fixed IP for the life of the load balancer.
  - It also consists of a Load Balancer that serves as the single point of contact for clients to distribute traffic and a listener that checks for connection requests from clients using the protocol and port that you configure.
  - A target group routes requests to one or more registered targets, such as EC2 instances, using the protocol and the port number that you specify. Network Load Balancer target groups support the TCP, UDP, TCP_UDP, TLS, QUIC, and TCP_QUIC protocols.

- **Functioning of Network Load Balancer** : A Network Load Balancer functions at the fourth layer of the Open Systems Interconnection (OSI) model. It can handle millions of requests per second. After the load balancer receives a request from a client, it selects a target from a target group in the default action. It attempts to send the request to the selected target using the protocol and port that you specified.
  - When you enable an Availability Zone for the load balancer, Elastic Load Balancing creates a load balancer node in the Availability Zone. By default, each load balancer node distributes traffic across the registered targets in its Availability Zone only. If you enable cross-zone load balancing, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones.
  - To increase the fault tolerance of your applications, you can enable multiple Availability Zones for your load balancer and ensure that each target group has at least one target in each enabled Availability Zone. For example, if one or more target groups does not have a healthy target in an Availability Zone, we remove the IP address for the corresponding subnet from DNS, but the load balancer nodes in the other Availability Zones are still available to route traffic. If a client doesn't honor the time-to-live (TTL) and sends requests to the IP address after it is removed from DNS, the requests fail.
    - _For TCP traffic_, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, destination port, and TCP sequence number. The TCP connections from a client have different source ports and sequence numbers, and can be routed to different targets. Each individual TCP connection is routed to a single target for the life of the connection.
    - _For UDP traffic_, the load balancer selects a target using a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, and destination port. A UDP flow has the same source and destination, so it is consistently routed to a single target throughout its lifetime. Different UDP flows have different source IP addresses and ports, so they can be routed to different targets.
    - _For QUIC traffic_, the load balancer selects a target using the Server ID specified in the Connection ID (CID). For initial connection attempts that lack a Server ID, a flow hash algorithm based on the protocol, source IP address, source port, destination IP address, and destination port is used. Once a Connection ID is established traffic for this CID gets routed to the same target for the lifetime of the CID.

- **Gateway Load Balancer** : Distributes traffic to a fleet of appliance instances. Provides scale, availability, and simplicity for third-party virtual appliances, such as firewalls, intrusion detection and prevention systems, and other appliances. Gateway Load Balancers work with virtual appliances that support the GENEVE protocol.

- **Functioning of Gateway Load Balancer** : Gateway Load Balancers enable you to deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. It combines a transparent network gateway (that is, a single entry and exit point for all traffic) and distributes traffic while scaling your virtual appliances with the demand.
  - A Gateway Load Balancer operates at the third layer of the Open Systems Interconnection (OSI) model, the network layer. It listens for all IP packets across all ports and forwards traffic to the target group that's specified in the listener rule.
  - It maintains flow stickiness to a specific target appliance using 5-tuple (default), 3-tuple, or 2-tuple. The Gateway Load Balancer and its registered virtual appliance instances exchange application traffic using the GENEVE protocol on port 6081.
  - Gateway Load Balancers use Gateway Load Balancer endpoints to securely exchange traffic across VPC boundaries. A Gateway Load Balancer endpoint is a VPC endpoint that provides private connectivity between virtual appliances in the service provider VPC and application servers in the service consumer VPC.
  - You deploy the Gateway Load Balancer in the same VPC as the virtual appliances. You register the virtual appliances with a target group for the Gateway Load Balancer.
  - Traffic to and from a Gateway Load Balancer endpoint is configured using route tables. Traffic flows from the service consumer VPC over the Gateway Load Balancer endpoint to the Gateway Load Balancer in the service provider VPC, and then returns to the service consumer VPC.
  - You must create the Gateway Load Balancer endpoint and the application servers in different subnets. This enables you to configure the Gateway Load Balancer endpoint as the next hop in the route table for the application subnet.

- **Classic Load Balancer** : Routes and load balances either at the transport layer (TCP/SSL), or at the application layer (HTTP/HTTPS).

| Load Balancer Type              | OSI Layer | Key Traffic Protocols | Best Use Case                                                               | Key Features                                                                                |
| ------------------------------- | --------- | --------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Application Load Balancer (ALB) | Layer 7   | HTTP, HTTPS, gRPC     | Modern web apps, microservices, and containerized APIs.                     | Path-based routing (e.g., /api vs /static), host-based routing, and SSL termination.        |
| Network Load Balancer (NLB)     | Layer 4   | TCP, UDP, TLS         | High-performance, ultra-low latency apps like gaming or financial platforms | Scales to millions of requests per second, provides static IP addresses per AZ.             |
| Gateway Load Balancer (GWLB)    | Layer 3   | IP packets            | Deploying and scaling third-party virtual appliances                        | Centralizes traffic routing through network security appliances like firewalls and IDS/IPS. |

- **Some algorithms used in Load Balancers** : Load balancing algorithms fall into two main categories - _static algorithms_ that follow fixed rules, and _dynamic algorithms_ that adapt to real-time server conditions
  - Static Algorithms :
    - Round Robin : Cycles sequentially through available servers in order. Best when servers have equal capacity and similar workloads.
    - Weighted Round Robin : Assigns weight values based on server capacity so stronger servers handle more requests.
    - IP / URL Hash : Uses a hash function on the client's IP address or request URL to map requests to a specific server. Useful for session persistence (sticky sessions) and caching.
    - Random : Picks an available server at random from the pool. Simple and effective under high traffic
  - Dynamic Algorithms :
    - Least Connections : Sends new requests to the server with the fewest active connections. Helpful when requests vary in processing time.
    - Weighted Least Connections : Combines active connection counts with assigned server weights to balance load across uneven hardware.
    - Least Response Time (or Weighted Response Time) : Routes traffic to the server with the fastest response time and lowest active load to minimize latency.
    - Resource-Based : Queries real-time server metrics—such as CPU, memory, or I/O—to distribute traffic based on actual available resources.
    - Least Bandwidth : Directs traffic to the server currently using the least network bandwidth.

---

### **AWS EC2 Auto Scaling & Auto Scaling Groups**

- Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application. You create collections of EC2 instances, called _Auto Scaling groups_.
- An Amazon EC2 Auto Scaling group is a collection of Amazon EC2 Auto Scaling instances that are managed and scaled automatically as a single unit.
- The goal of an Auto Scaling Group (ASG) is to:
  - Scale out (add EC2 instances) to match an increased load
  - Scale in (remove EC2 instances) to match a decreased load
  - Ensure we have a minimum and a maximum number of machines running
  - Automatically register new instances to a load balancer
  - Replace unhealthy instances

  ![AutoScalingGroup](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/asg-basic-arch.png)

**Core Concepts of Auto Scaling Groups** :

- Capacity Limits : You define a minimum size, maximum size, and desired capacity for the group. The group will never drop below the minimum or exceed the maximum limits.
  - Minimum Size : The minimum number of instances in each Auto Scaling group ensures that your group never goes below this size.
  - Maximum Size : The maximum number of instances in each Auto Scaling group ensures that your group never goes above this size.
  - Desired Capacity : The desired capacity, either when you create the group or at any time thereafter, ensures that your group has this many instances.
- Launch Templates : The group uses a launch template to specify instance configuration details, such as the Amazon Machine Image (AMI), instance type, security groups, and key pairs.
- Health Checks : Periodic health checks monitor instances and automatically terminate and replace any unhealthy instances to maintain the desired capacity.
- Availability Zones : Capacity spreads automatically across multiple Availability Zones (AZs) to improve application reliability and fault tolerance.
- Scaling Policies : Dynamic scaling policies, schedules, or manual adjustments launch or terminate instances in response to changing application traffic and CPU or memory load.
- Default Limits : By default, an Auto Scaling group can manage up to 200 EC2 instances, though this quota can be increased via AWS support.
- Automated replacement of Spot Instances : If your group includes Spot Instances, Amazon EC2 Auto Scaling can automatically request replacement Spot capacity if your Spot Instances are interrupted. Through Capacity Rebalancing, Amazon EC2 Auto Scaling can also monitor and proactively replace your Spot Instances that are at an elevated risk of interruption.
- Load balancing : You can use Elastic Load Balancing load balancing and health checks to ensure an even distribution of application traffic to your healthy instances. Whenever instances are launched or terminated, Amazon EC2 Auto Scaling automatically registers and deregisters the instances from the load balancer.
- Scalability : Amazon EC2 Auto Scaling also provides several ways for you to scale your Auto Scaling groups. Using auto scaling allows you to maintain application availability and reduce costs by adding capacity to handle peak loads and removing capacity when demand is lower. You can also manually adjust the size of your Auto Scaling group as needed.

_Some advanced features of EC2 Auto Scaling_ :

- Instance refresh : The instance refresh feature provides a mechanism to update instances in a rolling fashion when you update your AMI or launch template. You can also use a phased approach, known as a canary deployment, to test a new AMI or launch template on a small set of instances before rolling it out to the whole group.
- Lifecycle hooks : Lifecycle hooks are useful for defining custom actions that are invoked as new instances launch or before instances are terminated. This feature is particularly useful for building event-driven architectures, but it also helps you manage instances through their lifecycle.
- Support for stateful workloads : Lifecycle hooks also offer a mechanism for persisting state on shut down. To ensure continuity for stateful applications, you can also use scale-in protection or custom termination policies to prevent instances with long-running processes from terminating early.

  ![AutoScalingWithLoadBalancer](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/elb-tutorial-architecture-diagram.png)

**_Auto Scaling Groups – Scaling Strategies_** : An Auto Scaling Group (ASG) scaling strategy automatically adjusts the number of running instances to match application demand, balancing performance, availability, and cost. ([Read More about this](https://www.nops.io/blog/aws-auto-scaling-benefits-strategies/))

- Target Tracking Scaling : Maintains a specified metric—such as average CPU utilization (e.g., 50%) or request count per target—at a target value by adding or removing instances.
- Step and Simple Scaling : Triggers scaling actions based on CloudWatch alarms when static metric thresholds are crossed.
  - Simple scaling applies a specific adjustment (e.g., add 2 instances) and waits for a cooldown period.
  - Step scaling applies varying adjustments based on the size of the alarm breach.
- Scheduled Scaling : Proactively scales capacity up or down based on predictable time-and-date schedules (e.g., scaling out before a daily peak-hour traffic surge).
- Predictive Scaling : Uses machine learning to analyze historical traffic patterns and automatically provisions or deallocates instances before the demand spike occurs.
- Manual Scaling : Manually overrides and updates the group's minimum, maximum, or desired capacity directly via the console or CLI.
