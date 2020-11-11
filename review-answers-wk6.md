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


