#### Have you used Scala?

#### Have you used hadoop?

#### Have you used Hive?

#### Have you used Spark?

#### Have you used Kafka?

#### ACID compliance - database transaction
- Atomicity refers to the integrity of the entire database transaction being one unit.  Atomicity guarantees that the entire transaction 
will be performed as if it were a single operation.  That is, all changes will be performed or none of them.

- Consistency refers to the state of data when a transaction starts, and when it ends.  A transaction must follow the rules of the
database, else it be rolled back to a state which does comply.

- Isolation is the property that ensures that concurrent transactions that are reading and writing to a table at the same time leave
the database in serialized state and as if they were run sequentially.

- Durability is the property that guarantees that once a transaction is successfully committed, it will endure system failures and 
changes to data will persist.

*Strong consistency, focus on "commit", conservative, slower evolution (schema)*


#### BASE consistency model for distributed systems

- Basically Available - availablity is important and reading and writing operations trump consistency guarantees

- Soft state - Because consistency is not guaranteed and data can be in the process of sync'ing state may not match across replications

- Eventual consistency - The data will eventually sync, and will continue to move in to a state of consistency, but as long as data is added, it will be evolving.

*Availability first, best effort, approximate answers should be ok and aggresive.  Simpler, faster, easier evolution.*

#### CAP Theorem - distributed systems (aka Brewer's theorem)

- Consistency - All clients - same data, same time, all nodes.  Every read request gets most recent write or error.  

- Availability - Every request get non-error response, without guarantee is most recent write.

- Partition tolerance - Nodes containue to work, regardless of partitions (communications disruption).

#### Types of NoSQL databases: 

- CP database - Consistency and Partition tolerance, when partition occurs, not available. (ex: mongoDB)

- AP database - Availability and Partition tolerance, when partition occurs, available, but consistency not guaranteed. (ex: cassandra)

- CA database - Consistency and Availability, but cannot handle partitions/fault tolerance.  Not practical in distributed systems.




