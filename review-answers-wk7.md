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


#### How does new data arriving in a stream get represented in Spark Streaming? 
#### In Structured Streaming? 
#### What is Apache Kafka? 
#### What is Pub Sub? 
#### Client Server? 
#### Messaging queues? 
#### What are some advantages of pub sub? 
#### Why are those advantages especially relevant in large distributed applications? 
#### What are events in Kafka? 
#### What is a topic? 
#### A log? 
#### Where do events come from in Kafka? 
#### Where do they go? 
#### What are the machines in a Kafka cluster called? 
#### What are partitions in Kafka? 
#### How do partitions achieve HA and fault tolerance? 
#### What happens on machine failures in a Kafka cluster? 
#### What is Apache Zookeeper? 
#### What’s the difference between pulling and pushing messages/events in a pub sub architecture? 
#### Which does Kafka use? 
#### How long does Kafka store messages by default? 
#### What are our configuration options? 
#### What is Kafka Stream Processing? 
#### Does Kafka guarantee that it will preserve the order of produced events? 
#### What are the caveats? 
#### How can we make sure that Kafka preserves the order of events where it matters?
