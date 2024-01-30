Whenever your are designing a distributed data store, you have to think in terms of **tradeoffs**. An example of this being the the CAP theorem:

1. **Consistency:** All nodes see the same data at the same time. Consistency is akin to having a single up-to-date copy of the data.
    
2. **Availability:** Every request receives a response, without guaranteeing that it contains the most recent version of the information. 
    
3. **Partition Tolerance:** The system continues to operate despite arbitrary message loss or failure of part of the system. That is, the system can sustain any network failure that doesn't result in a failure of the entire network.
    

The theorem states that a distributed system can only provide two of these three guarantees simultaneously:

- **CA - Consistency and Availability without Partition Tolerance:** This is not a viable option for distributed systems, as network failure is a reality that cannot be ignored.
- **CP - Consistency and Partition Tolerance without Availability:** In the event of a partition, some parts of the system might become unavailable, but the system ensures data consistency across the partitions.
- **AP - Availability and Partition Tolerance without Consistency:** The system remains available under partitioning, but there might be inconsistencies across the different partitions.
![[CAPTheorem.png]]

**Practical Implications:**

- When designing distributed systems, architects must decide which two attributes are most critical for their system's needs and make trade-offs accordingly.
- NoSQL databases often face these trade-offs, with different databases opting for different combinations of the CAP properties (e.g., Cassandra for AP, MongoDB for CP).
- Understanding the CAP theorem helps in making informed decisions about the system architecture in terms of data handling, network setup, and overall reliability