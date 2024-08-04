A core feature of [[system architecture]]. Being able to carry the task you need whenever you need them. It's the concepts of **reliability**, **Resilience** and **fault tolerance**. 
This is closely related to [[architecture/Quality attributes/security|security]] and [[Performance]]

the availability can be calculated with the equation
$A=\frac{M T B F}{MTBF+M T T R}$    Where 
A	=	availability
MTBF	=	mean time between failure
MTTR	=	mean time to repair
# Key concepts
As i said availability should not come alone. It must have this other concepts for true availability:
## Reliability
Ability to operate **without** **errors**. Your system should have all cases covered.
## Resilience
Being able to manage failures effectively. 
## Fault tolerance
Being able to **continue in operation**, even in case of failures
## SPOF
*S*ingle *P*oints *O*f *F*ailure should be eradicated. If these fail all of the system falls. There is no availability now


# Tactics
## detect tactics
- **monitor**. Checking the state of other parts of the system, like processors, processes, I/O, memory,
- **heartbeat**. The process is sending periodic messages to another [[server]], these messages can include the monitor tactic   
- **Sanity Checking**: Checking the answers that the components provide to predetermined questions, and checking that the answer never changes 
- **Voting**: When there are multiple distributed system, we take the decision that the most agree upon
- **self test**: Running a test on itself from time to time, can be initiated by the component itself or invoked  by a system monitor. The test can be normal unit test or checksums.
## recover from faults
- **Redundant Spare**: having spares ready to run if the current one isn't able to. 
- **rollback**: Returning to a previous known good state if the current one fails
- **Graceful Degradation**: leaving the important components alive while the less important are shot down. For example stop logging and sidecars if you run out of [[RAM]]
- **Shadow**: running process as a shadow, they are there but not fully advertised, this to check they work properly 
- **Replication** at **remote** sites: Your datacenter could have problems, network, natural disasters among others. If it's imperative your system must have a replicas in geographically distant places
- **Logging** and **Snapshots**: This applies mostly to [[mid level/databases/Database|Databases]] and in [[cloud computing]]. But these allow you to create a Snapshot (a full copy of all of the data including the database motor. Useful to create immediate new components based on your current) or they log all of the data. Making so you can rollback any changes just looking at the logs
## prevent faults
- [[relational database#ACID|Transactions]]: using the [[sql]] transactions system   
- Removal from Service: If possible restart some components sporadically, this makes memory leaks less likely 

# Patterns
common implementation of the previous tactics

- **Triple** modular **redundancy** (TMR): an implementation of Voting. Three modules do the same job, And they follow the majority
- **Process pairs**: doing checkpoints and rollbacks
## Redundant spare
having spares ready for running if the current one isn't able to. There are three of them
	- hot spare: it's running all the process that the main does. **Fastest**
	- warm spare: it's turned on, when you want just swap them. **Fast**
	- cold spare: it's not turned on, cold booting problem. **Slower**
