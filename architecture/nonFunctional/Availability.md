A core feature of [[system architecture]]. Being able to carry the task you need whenever you need them. It's the concepts of **reliability** and **recovery**. 
This is closely related to [[security]] and [[performance]]

the availability can be calculated with the equation
$A=\frac{M T B F}{MTBF+M T T R}$    Where 
A	=	availability
MTBF	=	mean time between failure
MTTR	=	mean time to repair

# tactics
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
## prevent faults
- [[relational database#ACID||Transactions]]: using the [[sql]] transactions system   
- Removal from Service: If possible restart some components sporadically, this makes memory leaks less likely 

# Patterns
common implementation of the previous tactics
- **Redundant spare**: having spares ready for running if the current one isn't able to. There are three of them
	- hot spare: it's running all the process that the main does. **Fastest**
	- warm spare: it's turned on, when you want just swap them. **Fast**
	- cold spare: it's not turned on, cold booting problem. **Slower**
- **Triple** modular **redundancy** (TMR): an implementation of Voting. Three modules do the same job, And they follow the majority
- **Process pairs**: doing checkpoints and rollbacks
