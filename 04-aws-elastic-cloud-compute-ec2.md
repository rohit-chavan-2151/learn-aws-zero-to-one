# <u>**Elastic Compute Cloud (EC2)**</u>

EC2 (Elastic Compute Cloud) is a cloud computing service provided by Amazon Web Services (AWS). EC2 is an on-demand computing service on the AWS cloud platform called instances. It allows users to rent virtual servers to run applications in the cloud. You pay only for what you use.

Amazon EC2 is one of the most widely used AWS services because it provides scalable and secure virtual servers in the cloud. Organizations use EC2 to host websites, deploy applications, run databases, and support enterprise workloads without investing in physical hardware. The name 'Elastic Compute Cloud' can be explained as,

- **Elastic** : You can easily increase or decrease the number of instances or their size as your needs change.
- **Compute** : It provides the processing power, memory, and storage for your workloads.
- **Cloud** : It runs on AWS's massive, global data center infrastructure.

### **Features of EC2**

- _Functionality_ : It provides a virtual computing platform to run operations, launch instances, and fully customize the environment. Enhances security and allows configuration changes at any time. Offers default AMIs and supports custom AMIs to be reused with existing/preferred configurations.
- _Operating Systems_ : Provides a wide selection of operating systems when choosing an AMI. Allows users to upload and use their own operating systems.
- _Software_ : Leads the cloud computing market with diverse EC2 options. Allows users to choose from a wide range of software for EC2 instances.
- _Scalability and Reliability_ : Handles dynamic traffic scenarios efficiently. Provides reliable performance through flexible volumes and snapshots. Allows scaling up or down based on changing workload requirements.

### **Core Components of EC2 Instance**

1. _**Amazon Machine Image (AMI)**_ : Amazon Machine Image (AMI) Provides thousands of AMIs from AWS, the community, and AWS Marketplace. It allows users to create custom AMIs for reuse and consistency. Acts as a software blueprint containing the operating system, patches, and required software.

- An Amazon Machine Image (AMI) is a template containing the software configuration (operating system, application server, and applications) required to launch an Amazon EC2 instance.
  - Every EC2 instance, whether one or thousands, starts as a clone of the selected AMI.
  - Every AMI packages a root volume template, launch permissions, and a block device mapping.
  - AMIs exist in a single AWS Region and must be explicitly copied to be used in another.
  - AMIs are created, registered, copied, and deregistered. Deregistering does not automatically delete the underlying EBS snapshot.
  - AMIs come from Amazon, the AWS Marketplace, the community, or your own custom builds.
- Core Components of AMI :
  - Root Volume Template : A snapshot of the root volume (typically EBS) containing the OS and all installed software.
  - Launch Permissions : Controls which AWS accounts are authorized to use the AMI to launch instances.
  - Block Device Mapping : Specifies which volumes (root and any additional storage) are attached to the instance at launch.
  - The AMI storage types comes in two types - **EBS-Backed AMI** & **Instance Store-Backed AMI**

2. _**EC2 Instance Types**_ : Instance types are the hardware profiles of your virtual server. AWS offers a vast array of instance types optimized for different tasks, grouped into families.

- **t family (e.g., t2.micro, t3.large)** : General Purpose, burstable instances. Perfect for web servers, development environments, and small databases.
- **m family (e.g., m5.xlarge)** : General Purpose, balanced instances with a good mix of CPU, memory, and networking.
- **c family (e.g., c5.large)** : Compute Optimized, with a high ratio of CPU power to memory. Ideal for CPU-intensive tasks like batch processing, media transcoding, and scientific modeling.
- **r family (e.g., r5.large)** : Memory Optimized, with a high ratio of memory to CPU. Used for memory-intensive applications like large databases or in-memory caches.
- **g family (e.g., g4dn.xlarge)** : GPU-based instances designed for machine learning, graphics processing, and video rendering.

3. _**Elastic Block Store (EBS) Volumes**_ : Elastic Block Store (EBS) provides durable, block-level storage attached to EC2 instances. It acts as a virtual hard drive for storing data. It persists data independently and can be detached and reattached to different instances

4. _**Security Groups**_ : A security Group acts as a virtual firewall for your EC2 instance, controlling all inbound and outbound traffic. You define rules that specify which protocols (e.g., SSH, HTTP), ports (e.g., 22, 80), and IP address ranges are allowed to send traffic to or receive traffic from your instance.

5. _**Key Pairs**_ : A Key Pairs consisting of a public key and a private key, is the set of security credentials used to prove your identity when connecting to a Linux EC2 instance. AWS stores the public key, and you are responsible for securely storing the private key file (.pem). You will use this private key to SSH into your instance.
