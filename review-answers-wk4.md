

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

CREATE TABLE STATES
	(NAME STRING,
	CAPITAL_CITY STRING,
	POPULATION INT,
	AREA DECIMAL,
	FOUNDING_YEAR DATE)
	ROW FORMAT DELIMITED
	FIELDS TERMINATED BY ', '
	TBLPROPERTIES("skip.header.line.count"="1");

#### load data into a table?
local filesystem:
LOAD DATA LOCAL INPATH "/home/dannylee/file.csv" INTO TABLE STATES;
hdfs:
LOAD DATA INPATH "/user/dannylee/file.csv" INTO TABLE STATES;

#### query data in a table?

SELECT * FROM STATES
ORDER BY FOUNDING_YEAR DESC
LIMIT 50;

#### filter the records from a query?

SELECT NAME, CAPITAL_CITY FROM STATES
WHERE POPULATION>100000000
ORDER BY FOUNDING_YEAR DESC;

#### group records and find the count in each group?

#### write the output of a query to HDFS?

#### specify we're reading from a csv file?


### Spark : Cluster Computing with Working Sets
#### What does Cluster Computing refer to?
#### What is a Working Set?
#### What does RDD stand for?
#### What does it mean when we say an RDD is a collection of objects partitioned across a set of machines?
#### Why do we say that MapReduce has an acyclic data flow?
#### Explain the deficiency in using Hive for interactive analysis on datasets.  How does Spark alleviate this problem?
#### What is the *lineage* of an RDD?

#### RDDs are lazy and ephemeral.  What does this mean?

#### What are the 4 ways provided to construct an RDD?

1. From a file in a shared FS - contents of a file
2. Parallelizing a Scala collection - taking a data structure and dividing it into slices
3. Transforming an existing RDD - we get a dataset produced by a transformation on the prior RDD
4. Change the persistence of an existing RDD - we get the cached version of the prior dataset which enables efficient processing.  Uses memory, and creates memory pressure.

#### What does it mean to transform an RDD?



#### What does it mean to cache an RDD?

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

#### Transformation

#### lineage

#### cache

#### lazy evaluation

#### broadcast variable

#### accumulator
