## Review:

#### In broad terms, what is a Join?
#### How does a shuffle hash join work in Spark?
#### How does a broadcast join work in Spark?
#### Why are broadcast joins significantly faster than shuffle joins?
#### Why can't we always use broadcast joins?
#### What is Spark SQL?
#### How does Spark SQL relate to the Spark applications we've been writing, using RDDs?
#### How does Spark SQL evaluate a SQL query?
#### What is the catalyst optimizer?
#### Why are there multiple APIs to work with Spark SQL?
#### What are DataFrames?
#### What are DataSets?
#### How are DataFrames and DataSets "unified" in Spark 2.0?
#### What is the SparkSession?
#### Can we access the SparkContext via a SparkSession?
#### What other contexts are superseded by SparkSession?
#### What are some data formats we can query with Spark SQL?
#### Are DataSets lazily evalauted, like RDDs?
#### What are some functions available to us when using DataFrames?
#### What's the difference between aggregate and scalar functions?
#### How do we convert a DataFrame to a DataSet?
#### How do we provide structure to the data contained in a DataSet?
#### How do we make a Dataset queryable using SQL strings?
#### What is the return type of spark.sql("SELECT * FROM mytable") ?
#### How do we see the logical and physical plans produced to evaluate a DataSet?


#### Broadcast Joins
(aka Map-side Joins or broadcast hash join)

spark.sql.autoBroadcastJoinThreshold - max. size (in bytes) for a table that will be broadcast to all worker nodes when performing a join). 
- default: 10L * 1024 * 1024 (10MB)

Broadcast joins can be very efficient for joining a relatively small table with a larger table, by avoiding the need to shuffle and send the large table over the network. 

```
val q = large.join(broadcast(small), "id")
val plan = q.queryExecution.logical
scala> println(plan.numberedTreeString)

00 'Join UsingJoin(Inner,List(id))
01 :- Range (0, 100, step=1, splits=Some(8))
02 +- ResolvedHint (broadcast)
03    +- Range (0, 1, step=1, splits=Some(8))
```

Deep dive into joins: https://www.oreilly.com/library/view/high-performance-spark/9781491943199/ch04.html

Image below from https://www.slideshare.net/databricks/new-developments-in-spark

![shuffle](images/1-shuffle.jpg)

![broadcast](images/2-broadcast.jpg)

![hybrid-a](images/3-hybrid-a.jpg)

![hybrid-b](images/4-hybrid-b.jpg)

---

#### SBT overview 
- https://www.slideshare.net/hermannhueck/pragmatic-sbt


--- 
#### Catalyst and Spark SQL

The Catalyst extensible query optimizer helps develop a physical plan to select the lowest-cost plan for processing data.  The sequence of events is:
- unresolved logical plan
- reads catalog and generates a logical plan
- creates an optimized logical plan
- creates multiple physical plans
- evalutes the best solution usijg cost method
- selects a physical plan
- generates RDDs

#### Dataframes and Datasets

DataFrames have named columns and a structure like SQL/collection tables.  They hold data in records and have columns with datatypes.

DataSets are between DataFrames and RDDs, they contaiun strongly typed collections of distributed data.  Content of a DataSet is typically a Scala case class.  

They are both distributed collections of data that are processed using the catalyst optimzer to convert them to RDD.  

In Spark 2.0 they are unified and DataFrame is just a DataSet that contains generic Row objects instead of specific Scala case classes.

ex: DataSet[Comic] - a dataset of comics, DataSet[Person] a dataset of persons, DataSet[Row] means a dataset containing generic Rows - or a DataFrame.  We can also call DataFrames "untyped DataSets".




