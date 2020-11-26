#### What is Spark Streaming? 

Spark Streaming is an extension built on top of core Spark, which provides scalable, high-throughput, fault-tolerant stream processing of live data streams.  These streams of data can come from sources like Kafka, HDFS/S3, Kinesis or TCP sockets (Twitter/Apis) and processed with the high-level functions like map, reduce, join and window.  The processed data can be sent out to filesystems, databases or dashboards.

Spark Streaming breaks live input data into batches (user configured) and provides an abstraction called DStreams (discretized streams) which represent a continuous stream of data.  We access the APi through the StreamingCOntext

Transformation methods on DStreams: map, flat map, filter, reparition, union, count, reduce, countByValue, reduceByKey, join, cogroup, transform, updateStateByKey.

Window transformation operations: window(windowLength, slideInterval), countByWindow, reduceByWindow, reduceByKeyAndWindow

note: reduceByKeyAndWindow's given function needs to be associative (grouping doesnt affect result) and commutative (order of operations doesn't matter)

Output operations on DStreams: print(10), saveAsTextFiles, saveAsObjectFiles, saveAsHadoopFiles, foreachRDD

#### What is Spark SQL? 

Spark SQL is a spark module for structured data processing.  Spark SQL provides an abstraction to work with RDDs in a way that is accessible for those with knowledge of SQL.  It also adds some optimizations to how data is queried because internally it understands the structure of the data and what computations are being performed.  It can be more efficient to use than the working directly with low-level RDDs, through the use of the Catalyst optimizer.  Once we write our SQL query, the query is taken by the Catalyst optimizer which then produces a logical plan based on the table and views (held in the catalog) and produces multiple physical plans.  It then selects the most efficient (lowest cost) model and executes the plan using RDDs.

Spark SQL can be used to read and make SQL queries on Hive tables.  DataFrames and DataSets can be used in SparkSQL, DFs are like tables in SQL and hold data as records, with columns.  DataSets containg data in a strongly typed, and usually in a Scala case class.  Since Spark 2.0, Spark SQL DFs are DS's that are holding data in Rows, rather than a case class.

#### What is Structured Streaming? 

Structured streaming is built on top of the Spark SQL engine and gives you the DataSet/DatAFrame API functionality to work on streaming computations.  It provides the optimization benefits of the Spark SQL engine and end-to-end exactly once, fault-tolerance through checkpointing and write-ahead logs.  (Write-ahead logs are a technique used to provide atomicity and durability.  By logging the change to stable storage before performing the operation, in the case of power failure the system will know whether it needs to rollback, complete or keep the changes made.  Checkpointing is writes application state to reliable storage (HDFS) and saves data like Metadata, configurations, DStream operations and incomplete batches, as well as Data checkpointing intermediary RDDs to save time to recover them.)

Structured streaming processes data streams as a series of batch jobs and can achieve latencies as low as 100 ms, and exactly-once fault-tolerance guarantees.

There are three modes for **output**: 
- complete: Entire result table will be writte to the external storage.
- append: Only new rows appended in the result table since the last trigger will be written.
- update: Only the rows that were updated in the result table since the last trigger will be written.

Input sources:
- file source
- kafka source
- socket source (testing)
- rate source (testing)

Output Sinks:
- File sink - stores to directory
- Kafka sink - stores to one or more topics in Kafka
- Foreach sink - runs computations on each record
- console sink (testing) - print to console
- memory sink (testing) - store as in-memory-table

#### How does new data arriving in a stream get represented in Spark Streaming? 

In Spark streaming, new data is treated as an RDD.  The DStream is a continuous series of RDDs.

#### In Structured Streaming? 

In structured streaming, new data is added as new rows being appended to the Input table.  The Spark queries are run as an *incremental* query on the *unbounded* input table.

#### What is Apache Kafka? 

Apache Kafka is a distributed, horizontally scaling, elastic, fault-tolerant and secure system to provide event streaming and processing.  It is built to reliably publish and subscribe to stremas of events and import/export that data to other systems.  It can store streams of events and it can process those streams on the fly or retrospectively. 

#### What is Pub Sub? 

Pub sub is a design pattern to decouple publishers from subscribers, meaning that publishers don't need to know their subscribers and subscribers don't need to know about the publishers.  Instead they speak through topics or channels.  A single application can publish and/or subscribe to multiple topics and both publishers and subscribers can asynchronously produce events and process events.  Pub Sub also provides durable message storage and real-time delivery with high availability and scalability.

Its used for:
- Balancing workloads on network clusters: large queue of tasks can be efficiently distributed among multiple workers.
- Implementing async workflows: an order processing app can place an order on a topic which can be processed by one or many workers
- Distributing event notifications: a service that accepts user signups can send notification when a new user registers and downstream services can subscribe to receive notifications of the event
- Refreshing distributed caches: An app can publish invalidation events to update the ids of objects that have changed 
- Logging to multiple systems: A single VM instance can write logs to a monitoring system, a database for later querying, pagerduty, etc

#### Client Server? 

Is a distributed application structure that separates taks or workloads between providers of a resource or service, aka servers,  and the requesters (consumerss), aka clients.  In a typical client-server model, there is a request-response messaging pattern.  This interactive communication requries the direct connection between client-server.

#### Messaging queues? 

A mq provides an aysnchronous communications protocol which provides a queue of messages sent between applications.  A queue is a line of waiting things that need to be handled. A message is the data between sender and receiver.  The idea is that queue holds messages, until the consumer is ready to retrieve them.  It decouples the producer from the consumer. 

#### What are some advantages of pub sub? 

The difference with pub-sub is that pub-sub allows multiple consumers to receive each message in the topic, pub-sub also holds the list of messages in order for other consumers, who can pick up from the beginning.  Where as with MQs once a message is consumed it removed from the system.
 
#### Why are those advantages especially relevant in large distributed applications? 

It provides high availablity and resiliency, and the ability to scale elastically.  By being able to generate new brokers to handle queries and to regenerate a list of messages in a topic pub-sub provides a way to recover from system failures.

#### What are events in Kafka? 

Events (aka record or message) is made up of a key, value, timestamp and metadata.  They are written in batches (record batch), which contain one or more records.

#### What is a topic? 

A topic is like a folder where each the files are events.  Topics are multi-subscriber and multi-producer, and can have 0, 1 or more producers that write events and 0, 1 or more consumers who subscribe to it.  After the events are consumed they remain for a configured amount of time.

Topics are partitioned over a number of buckets located on different kafka brokers.  They are also replicated (3 is common).

#### A log? 

The log for a topic consists of N number of directories for N number of partitions of a topic.  Inside the folder are datafiles that contain the messages of that topic, whose 64-bit integer offset ids provide the position of the message in terms of all the messages ever sent to the topic.  The log provides durability by writing the messages to disks after M messages or S seconds between disk flushes.  In case of recovery from failure, the log recovery process reads over each entry and validates that the CRC32 of the message payload matches CRC stored with the message.  It then truncates the log to the last valid offset.

#### Where do events come from in Kafka? 

The producer sends data to the leader broker for the partition, and this broker can be reached through any of the Kafka nodes because they all know which servers are alive and where the leaders for the partitions of a topic are at any time.  

#### Where do they go? 

The messages are stored on the brokers after being partitioned by the leader broker.  They can either be partioned at random, or done by some semantic partitioning function.  A key can be specified to partition by and using this hash to partition, all data with the same key will arrrive at the same partition.

#### What are the machines in a Kafka cluster called? 

The machiens of a Kafka cluster are called brokers and some act as the storage layer, others run Kafka connect.

#### What are partitions in Kafka? 

Topics are partitioned (spread over buckets on different brokers).  This distributes the place of data to provide scalability and ability to recover from any failures in infrastructure.

#### How do partitions achieve HA and fault tolerance? 

Topics can be replicated to provide HA and fault-tolerance, by setting a replication factor of 3 there will always be 3 copies of data at the topic-partition level.   The leader of a partition will handle all reads and writes, and the number of replicas will dictate how many followers there will be.  These followers will consume messages from the leader just like any other consumer and apply them to their own log.

#### What happens on machine failures in a Kafka cluster? 

Machines must maintain a session with ZooKeeper via heartbeat and if it is a follower, it must replicate the leaders writes and not fall too far behind.  If the follower dies, gets stuck or falls behind the leader will remove it from the list of in sync replicas.  Each Kafka partition has a replicated log, and when a leader dies, a new leader is chosen from the followers.  Kafka ensures that a set of ISRs are caught-up to the leader, an are eligible for election.  A write to the Kafka partition is not considered committed until *all* ISRs have received the write.  If all ISRs die, two behaviors can be implemented, wait for a replica in the ISR to come back to life, choose the first replica (not necessarily in the ISR) that comes back to life.

#### What is Apache Zookeeper? 

Zookeeper is a centralized service for maintaining configuration information, naming, providing distributed syncronization and providing group services.  Its built for distributed applications and provides a set of primitives that can built upon to build more robust, less brittle software and avoid race conditions and deadlock.

In Kafka, Zookeeper stores its metadata like paritition location and topics configuration.  In 2019 a plan was made to integrate metadata management within Kafka.

#### What’s the difference between pulling and pushing messages/events in a pub sub architecture? 

Pulling messages allows consumers to decide when to retrieve messages, and ack that it received it.  In push delivery, the publisher initiates the sending of the message and the endpoint acks the message by returning an HTTP success code.  

Push is good for multiple topics that must be processed by a webhook.  Pull is good for large volume of messages and where efficiency and throughput of processing is critical.

#### Which does Kafka use? 

In Kafka, scalability was the driving factor for pull architecture.  Large numbers of consumers can subscribe without performance degrading.  Kafka can handle events at 100k per second from producers, so consumers can pull data at different paces and can either process in real-time or catch up when it can.

#### How long does Kafka store messages by default? 

168 hours or 7 days. (Topic configuration setting: `retention.ms`)

#### What are our configuration options? 

for zookeeper: the configuration file
`$ bin/zookeeper-server-start.sh config/zookeeper.properties`

for kafka broker service: the configuration file
`$ bin/kafka-server-start.sh config/server.properties`

#### What is Kafka Stream Processing? 
#### Does Kafka guarantee that it will preserve the order of produced events? 
#### What are the caveats? 
#### How can we make sure that Kafka preserves the order of events where it matters?
