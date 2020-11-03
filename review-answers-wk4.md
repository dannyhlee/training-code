

## Miscellaneous Notes

### Configuration files for yarn & hdfs

##### Hadoop
1. **hadoop-env.sh**: Environment variables that affect JDK used by Hadoop daemon.
2. **core-site.xml**: Config file for runtime environment of Hadoop cluster.  Informs where the NAMENODE runs and IP/port information.
3. **hdfs-site.xml**: Config file that contains NAMENODE, DATANODE, SECONDARYNODE settings, default block replication.
4. **mapred-site.xml**: Contains configuration settings for MapReduce.  We can specify framework name (MapReduce.framework.name)

#### yarn
1. **yarn-site.xml**: Configures HA for YARN, length of time before considering YARN node manager unavailable, idle time
2. **resource-types.xml**: Configures list of addiutional resources
3. **node-resources.xml**: 

https://docs.cloudera.com/HDPDocuments/HDP2/HDP-2.1.3/bk_using-apache-hadoop/content/configuration_files.html

---

### Datatypes inputs for mapper and reducer

#### Types of InputFormat in MapReduce:
Referenced from: https://data-flair.training/blogs/hadoop-inputformat/

1. **FileInputFormat** - Base class of all file-based input formats.  Specifies input directory where data files are located, reads files and divides into one or more inputSplits.
2. **TextInputFormat** - The default InputFormat, each line is treated a separate record, useful for line-based records like log files.  **Key** - LongWritable is the byte offset from the beginning of the file.  **Value** - the contents of the line, excluding line terminators.
3. **KeyValueTextInputFormat** - Similar to TextInputFormat.  Treats each line as a record.  **Key**  is everything up to tab ('\t'), **Value** is everything after.
4. **SequenceFileInputFormat** - Reads sequence files, which are binary and stores sequences of binary k-v pairs.  Sequence files block-compress and provide direct serialization and deserialization of several arbitrary data types.  Key and value are user-defined.
5. **SequenceFileAsTextInputFormat** - Like SequenceFileInputFormat, except that it converts the sequence file key values to Text objects by calling toString().   Makes sequences files suitable for streaming.
6. **SequenceFileAsBinaryInputFormat** - a SequenceFileInputFormat which we can extract the file's K-Vs as opaque binary object.
7. **NLineInputFormat** - Another TextInputFormat, keys are byte offset of tthe line and values are contents of the line.  If we want our mapper to received a fixed number of lines, we use NLineInputFormat.  Standard TextInputFormat will split by size and length of the lines, not number of lines.
8.**DBInputFormat** - is an InputFormat that reads data from a RDB, using JDBC - Java Database Connectivity.  Does not have portioning, so best for smaller datasets - key is LongWritable and Value is DBWritables.

---

## Review Questions
### Hive
#### What is Hive?

Hive is an open source data warehouse software for reading, writing and managing large data set files stored in HDFS or other data storage system such as Apache HBase.  Using a SQL like query language (HQL) data can be queryed using MapReduce, using SQL-like statements.

#### Where is the default location of Hive's data in HDFS?

Hive  default location for storing data is in /user/hive/warehouse under directories with the database name and table name as subdirectory names.

#### What is an External table?

We can store TBs of data outside of Hive to make it easier to store, but we can still query them by creating an external table.  The metadata/schema is described by external files and other processes can access the data outside of hive.  These can be stored on HDFS, or other cloud storage.

#### What is a managed table?

A managed table is one which is internal to Hive, where it owns the data.  The data, its properties and layout can only be accessed via Hive

#### What is a Hive partition?

Hive partitions allow us to division our data in a way that breaks the data set into smaller, logically organized pieces.  By splitting on data that we are interesting on querying and working with (generally with low cardinality) we can partition the data into chunks that make our data processing more efficient because we can skip blocks of data that don't fit into our column/columns.

#### Provide an example of a good column or set of columns to partition on.

A good column or set of columns to partition on are ones with low cardinality (low number of different choices in the set) and that we are interested in.  we want to be able break the data down into smaller chunks by this division so a column of states if we are working with state-level data would help us focus on one state or group of states, rather than the whole country.

#### What's the benefit of partitioning?

The benefits are filtering out datasets that will not fit our requirements from the start.  By dividing our data into logical partitions we can drop whole subsets of data and just work with relevant data.

Some disadvantages are number of HDFS files increases, number of intermediate files increases.  The metastore scales with the number of partitions.

#### What does a partitioned table look like in HDFS?

A partitioned table is a set of folders where the subdirectories are named by column and its specific range.  For example, if the column we were partitioning on was the state column, we might see "state=nd" or "state=sd" and inside that folder would a file with the subset of data that matched.

#### What is a Hive bucket?

A Hive bucket also divides our data into subsets.  However, in this case we choose columns of high cardinality and that do not mean that much to me.  Its used when we want to break our data into smaller chunks, but have a more randomized representation of the larger data set.

We can also skew on data that should be broken out to a separate directory, because hive creates one directory per skewed key with all remaining keys going into a separate bucket.

#### What does it mean to have data skew and why does this matter when bucketing?

Data skewing will break our data into lopsided buckets.  We can use this to our advantage if we have some oversized datasets, for example in states, we might have a key for the high population states (CA, TX, FL, NY) and then put the rest of the states in the "rest" group.

#### What does a bucketed table look like in HDFS?

The data is separated into separate folders by the skewed key or column's data like in with partitions.

#### What is the Hive metastore?

The metastore is a relational database that holds Hive's metadata of persistent relational entities (databases, schema, tables, columns, partitions).  It includes info like their structure and relationships.

#### What is beeline?

Beeline is a command line interface used to access hive server 2.  

### Hive Syntax questions: How do we....

#### create a table?
```
CREATE TABLE STATES
	(NAME STRING,
	NAME REGION,
	CAPITAL_CITY STRING,
	POPULATION INT,
	AREA DECIMAL,
	FOUNDING_YEAR DATE)
	ROW FORMAT DELIMITED
	FIELDS TERMINATED BY ', '
	TBLPROPERTIES("skip.header.line.count"="1");
```
#### load data into a table?
local filesystem:
```
LOAD DATA LOCAL INPATH "/home/dannylee/file.csv" INTO TABLE STATES;
```
hdfs:
```
LOAD DATA INPATH "/user/dannylee/file.csv" INTO TABLE STATES;
```

#### query data in a table?
```
SELECT * FROM STATES
ORDER BY FOUNDING_YEAR DESC
LIMIT 50;
```
#### filter the records from a query?
```
SELECT NAME, CAPITAL_CITY FROM STATES
WHERE REGION='nw'
ORDER BY FOUNDING_YEAR DESC;
```
#### group records and find the count in each group?
```
SELECT NAME, COUNT(POPULATION) FROM STATES
GROUP BY REGION;
```
#### write the output of a query to HDFS?
INSERT OVERWRITE DIRECTORY '/user/hive/states'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'

#### specify we're reading from a csv file?

FIELDS TERMINATED BY ','

### Spark : Cluster Computing with Working Sets

#### What does Cluster Computing refer to?

Cluster computing refers to a distributed framework of inter-connect computers for computational intensive data processing using a combination of high availability, load balancing and high performance computers to compute data with cost efficiency, processing speed, expandibility and scalability.

#### What is a Working Set?

Is a dataset stored in memory so that processing can work on it efficiently.

#### What does RDD stand for?

Resilient Distributed Dataset.

#### What does it mean when we say an RDD is a collection of objects partitioned across a set of machines?

The dataset is split up, by default a hashcode is used to make the divisions, and stored on different cluster nodes on the system.  The partition is a logical chunk of a large distributed data set.

#### Why do we say that MapReduce has an acyclic data flow?

Acyclic means without cycles, a series of steps that move in a one way flow and don't return to the same step.  MapReduce follows a series of steps and generates immutable outputs and does not offer looping to work on data iteratively.

#### Explain the deficiency in using Hive for interactive analysis on datasets.  How does Spark alleviate this problem?

Hive needs to run mapreduce each time it is processing data, and that includes writing out to disk and reading from disk.  The disk IO is a bottleneck as as well as the lost time recalculating (in some cases) the same data over and over again.  Spark alleviates this by holding the data memory through caching and also providing a way to run iterative processes.

#### What is the *lineage* of an RDD?

The lineage of RDD is the chain of transformations on data that produced the RDD.  By keeping a history or "family tree" of how the RDD came to be, Spark is able to easily reproduce lost partitions.

#### RDDs are lazy and ephemeral.  What does this mean?

They are lazy in that they are not calculated until there is an Action done on them that produces a side effect or return results.  The RDD isn't processed until they are ready to be used.  

They are ephemeral in that they will only exist when they are needed and unless we prevent it, they will disappear after they are used.  We can use .cache or .persist to ask Spark to hold onto the RDD for longer, but it is a request and depends on available memory resources.


#### What are the 4 ways provided to construct an RDD?

1. From a file in a shared FS - contents of a file
2. Parallelizing a Scala collection - taking a data structure and dividing it into slices
3. Transforming an existing RDD - we get a dataset produced by a transformation on the prior RDD
4. Change the persistence of an existing RDD - we get the cached version of the prior dataset which enables efficient processing.  Uses memory, and creates memory pressure.

#### What does it mean to transform an RDD?

To transform an RDD is to  produce a new RDD from an existing one through a series of functions.  

#### What does it mean to cache an RDD?

Caching an RDD is keeping it persisted in memory to speed up processing and prevent recreation through its lineage.  If we know that we are going to use it again in the series of tasks we are performing we can request that spark keep it in memory.  

We can cache in four ways:
1. MEMORY_ONLY - default.  If not enough, recompute.
2. MEMORY_ONLY_SER - attempt to store it in memory serialized, requires less memory but more computer power to ser/deserialize it.
3. MEMORY_AND_DISK - attempt to store in memory but if not enough room, put it on disk.
4. MEMORY_AND_DISK_SER - as above, but stored serialized

#### What does it mean to perform a parallel operation on an RDD?

This is an "action" (reduce, collect, foreach) that causes your RDD to actually be evaluated.  Reduce, aggregate dataset to value, return to driver.  Map, return entire dataset to driver, foreach cases a side effect for each element in the collection. 

#### Why does Spark need special tools for shared variables, instead of just declaring, for instance, var counter=0?



#### What is a broadcast variable?

These are global, read only variables and are sent to each worker/task, rather than passing them in.

#### What is an accumulator?

Are variables used to bridge the gap between different scopes (local runtimes) if we defined local variables to act as counters, we would have trouble merging them together at the end of the operation.  We can use accumulators to "add" (or do another accumulating operation) for parallel sums.  Is this related to context and serialization?

#### How would the Logistic Regession example function differently if we left off the call to .cache() on the points parsed from file?


## Be comfortable enough with the following terms to recognize them:

#### RDD

#### Action

An action is an event that causes the RDD to be evaluated and produce a result or have a side effect.  (Reduce, collect, foreach)

#### Transformation



#### lineage

#### cache

#### lazy evaluation




#### broadcast variable
Broadcast variables are way to efficiently pass read-only values to each worker and task in the cluster.  These values are cached in memory on all nodes.
#### accumulator
Spark's workers don't share scope and run in separate jvms which cannot normally share state with one another.  The accumulators are variables that can only be added to such as counters or sums.

#### Why is it necessary for Spark to write to disk after a shuffle?

Because Spark's shuffles redistribute data that is grouped across partitions, and collocate them to one node to operate on them.  Certain mapping operations will not fit in memory and will need to be written to a file, which is read during the reduce phase.  Also, the intermediate files created by shuffle need to be written and stored until references to the RDDs are gone to preserve lineage.
