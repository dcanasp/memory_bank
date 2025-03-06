Cloud computing is a model for delivering computing resources, such as [[server]]s, storage, [[database]]s, [[networking]], [[software]], and analytics, over the internet ("the cloud"). This approach enables organizations to access and manage these resources on-demand without needing to own physical [[hardware]] or manage the underlying infrastructure.

The benefits of cloud computing include:

- **Scalability**: Resources can be easily scaled up or down based on demand, allowing businesses to handle varying workloads efficiently.
- **Cost-effectiveness for small users**:[[cloud computing#Pricing at scale|[1] ]] Pay-per-use pricing models reduce costs, as businesses only pay for what they use instead of investing in expensive infrastructure.
- **Elasticity**: The ability to grow or shrink resources at a moment notice. 
- **Global Reach**: Cloud providers offer data centers across the globe, enabling low-latency access to services and content delivery to users worldwide.
- **Automatic Updates and Maintenance**: Cloud services are continuously updated with new features and security patches without requiring manual intervention from users.
- **Disaster Recovery and Backup**: Cloud providers offer robust solutions for data redundancy and recovery in the event of data loss or infrastructure failure.
# Why Cloud Computing Might Be Disadvantageous

While cloud computing offers many advantages, there are also potential drawbacks:

- **Security Concerns**: Storing data off-premises can introduce security risks, as sensitive information is accessible over the internet. Ensuring data protection often requires additional security measures.
- **Downtime and Reliability**: Although cloud providers strive for high availability, outages can still occur, leading to potential service disruptions.
- **Vendor Lock-in**: Once integrated with a particular cloud provider's ecosystem, switching to another provider can be complex and costly due to differences in services and technologies.
- **Compliance and Data Residency Issues**: Regulatory requirements may limit where data can be stored or how it is accessed, complicating cloud adoption for some industries.
The main drawback though is price when scaling
## Pricing at scale

While cloud computing offers cost advantages for startups and small businesses due to its pay-as-you-go model, it can become **more expensive** than **traditional servers** as the **scale** increases [^2]

[^2]: When we talk about scale it could be millions of MAU

At a large scale, the cost of continuously paying for cloud resources can exceed the expenses associated with owning and maintaining dedicated hardware in a private data center. This is especially true for businesses with **predictable workloads**, where buying and managing their own servers can result in significant savings over time.

#### Pay-as-You-Go and Security Risks

The pay-as-you-go pricing model introduces another challenge: the risk of **unexpected costs** due to malicious activity. Cloud providers charge based on the resources consumed, regardless of whether that usage was legitimate or caused by malicious users. For instance, a [[some attacks#DDOS (Distributed Denial of Service)|DDOS]] attack can cause a surge in traffic, leading to increased resource usage and higher costs.

Cloud providers like [[aws]] offer services such as [[high level/cloud/aws/Security#Shield|Shield]] and [[high level/cloud/aws/Security#WAF|WAF]] to mitigate such threats. These services can detect and prevent many types of DDoS attacks, shielding the application from downtime and service disruption. However, the customer is still responsible for the **costs** associated with **using** these protection services, including any **additional resources consumed during the attack**. This means that even if the attack is successfully thwarted, the user may still receive a significant bill due to the extra charges for scaling up resources to handle the attack and the fees for Shield and WAF usage.

Therefore, while cloud platforms can help safeguard against attacks, the financial burden from increased usage fees and security services during large-scale incidents can be considerable.
# Cloud Service Models

Cloud computing services are broadly categorized into three models, which provide different levels of control and management over resources:

1. **Infrastructure as a Service (IaaS)**: Offering raw computing resources such as [[server]]s and the network infrastructure without having to manage it.
    
2. **Platform as a Service (PaaS)**: Offers a platform allowing customers to develop, run, and manage applications without dealing with the underlying infrastructure. It abstracts away the need to manage servers and operating systems, allowing developers to focus more on writing code and building applications.
    
3. **Software as a Service (SaaS)**: Delivers fully functional applications over the internet that end users can access. These applications are managed by the cloud provider, and customers don’t need to worry about infrastructure or platform management.     

# Major Competitors

The cloud computing market is dominated by major players, with [[aws]] and [[gcp]] being two of the top competitors. Other significant providers include Microsoft Azure, IBM Cloud, and Oracle Cloud.
