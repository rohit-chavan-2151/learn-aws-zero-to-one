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
