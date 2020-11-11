

#### What is the lineage of an RDD?

The lineage of an RDD is a graph of all the parent RDDs to this RDD.  It is the path of transformation as a logical execution plan.   Aka RDD operator graph or RDD dependency graph.  The logical execution plan (sequence of commands) implicitly defines a DAG of RDD objects that will be used later when an action is called.  When we read the lineage it should be from bottom up because it starts with earliest RDD (with no dependencies on other RDDs or refencing cached data) and ends with the RDD that produces the action that has been called.

https://books.japila.pl/apache-spark-internals/rdd/spark-rdd-lineage/


#### How can we see the Lineage?

We can view the lineage of an RDD by calling the toDebugString() method on it.  That method will return a string describing the RDD's lineage (aka DAG/logical plan) and its recursive dependencies.

A related Another way to  or the EXPLAIN statement.  The EXPLAIN statement used an HQL query by default provides information about the physical plan, but can be EXTENDED to show the:
1. parsed logical plan
2. analyzed logical plan
3. optimized logical plan
4. physical plan

http://spark.apache.org/docs/latest/sql-ref-syntax-qry-explain.html

#### What do the indentations mean in the printed lineage?

The indentations indicate a shuffle boundary/new stage.  The number in round brackets show the level of parallelism at this stage.

#### What is the logical plan?  The physical plan?

A logical plan describes what needs to be done without deciding how to do it, a physical plan describes what every node would do.  The physical plan is divided into stages, stages contain tasks.

#### How many partitions does a single task work on?

Each partition of the input data corresponds to one task.

#### What’s the difference between cluster mode and client mode on YARN?

##### Cluster Mode 
In contrast to client mode, Spark in Cluster mode will run the Driver as a subprocess of ApplicationMaster.  If the ApplicationMaster hosting driver fails, it can be re-instantiated on another node in the cluster.  Here, the client invokes spark-submit, and submits a Spark app to the CLuster Manager (Yarn's ResourceManager).  The ResourceManager assigns an ApplicationMaster (the Spark Master) for the app.  The Driver process is created on the same node.  The AM requests containers for Executors from RM, executors are spawned and establish contact with the Driver and returns progress, results and status.  The Driver in turn, redirects the progress, results and status to the client.

In Cluster mode spark runs inside an ApplicationMaster (acting as the Spark Master) in Yarn, output from our driver will appear inside the Yarn container created by ApplicationMaster by the ApplicationManager.  Cluster manager - An external service for acquiring resources on the cluster (e.g. standalone manager, Mesos, YARN).  The ApplicationMaster requests resources for Executors from the Resource manager.

##### Client mode
Initially, the Client submits a Spark app to the Cluster Manager (Yarn's ResourceManager).  The Driver process, SparkSession and SparkContext are created and run on the client.  Yarn's ResourceManager assigns an ApplicationMaster (the Spark Master) for the app.  The ApplicationMaster requests containers to be used as Executors from the ResourceManager.  Once the containers are assigned, the Executors are spawned and establish contact with the Driver to report progress, results and status to the Client.

In client mode, the Driver runs outside of YARN (on the Client, which is often on YARN's master node) and communicates with ApplicationMaster. Output appears in its current environment (often Yarn's master node).   If the Driver host fails, the application fails.

#### What is an executor?  What are executors when we run Spark on YARN?

An executor is a distributed worker that is coordinated by one central coordinator, the Driver.  In Yarn, executors are processes running on Worker nodes to handle tasks by running computations and storing data.  Once complete, the executor sends the results to the driver. 

The Driver contacts the cluster manager and requests resources for the Executors/Worker nodes.  The cluster manager launches the Executors.  The executors then establish connection with the Driver.  The driver determines the Tasks by checking the Lineage and create a logical and physical plan.  Once the physical plan is generated Spark allocates tasks to the Executors.  Tasks are run on the executors, and upon completion the results are sent back to the Driver.  When all tasks are complete, the main method on the Driver exits (invokes sparkSession.stop() - previously sparkContext, SQLcontext, HiveContext, StreamingContext).  Spark releases all resources from the Cluster manager.

#### What is AWS?

Amazon Web Services provides on-demand, scalable cloud computing solutions and along with GCP - Google Cloud Platform and MS Azure, they provide a wide range of solutions in scalable compute, database and server instances, storage (file, object, warehousing, data lakes), analytics, network/content delivery, machine learning capabilities.

#### EC2?

EC2 stands for Elastic Compute Cloud,  elastic respresents that the service is resizeble which can expand and contract according to need,  compute cloud means  compute capacity available in the cloud.  The EC2 offers virtual compute platforms with choice of processor (intel, amd and arm), storage, networking, operating systems and purchase models.  Instances can be optomized for compute, memory, accelerated computing and storage.  Interestingly AWS just announce Graviton2 ARM based processors, 64 vpucs, 25gbps networking 18gbs EBS bandwidth.

#### S3?

Amazon S3 (Simple Storage Service) provides object storage, each with its own key/id (aka Buckets).  Can be private or accessed programatically or through services like CloudFront (Amazon's CDN).  S3 is used as a data lake (structured and unstructured data store with scehma-on-read for ML, PA (predictive analytics) DD (Data discovery), backup and restoration (along with EBS, EFS or S3 glacier). S3 is secure and providing 11 nines of data durability 99.999999999.

#### EMR?

[Amazon Elastic MapReduce](https://aws.amazon.com/emr/) (EMR) is a fully managed PaaS solution for distributing and processing data from Amazon Web Service (AWS). With EMR, AWS customers can quickly spin up multi-node Hadoop clusters to process big data workloads.  EMR has tools like Hive and Spark and offers horizontally scaling on EC2 instances.  Elastic and available on demand, with the ability to easily spin up and spin down clusters and paying for what you use without the cost of building your own infrasturcture.  Able to handle massive data loads.

#### What does it mean to run an EMR Step Execution?

When launching an EMR cluster the default setting for **Launch mode** is "Cluster".  The "Cluster" option indicates specifies that we want what's called a "long-running cluster".  It will not terminate once the job is finished and will continue to run.  By changing the **Launch Mode** option to "Step Execution" the cluster will terminate after executing.  This "auto-termination  is the default when we launch EMR through the EMR API.

When a cluster terminates all Amazon EC2 instances in the cluster terminate and the data in the instance store and EBS (Elastic Block Store) volumes are no longer available or recoverable.  This makes it important to set a `--log-uri` parameter when running `create-cluster` to direct log output to an S3 instance for access after the job is finished and the cluster has been terminated.

```aws emr create-cluster --name "Test cluster" --release-label emr-4.0.0 --log-uri s3://mybucket/logs/ --applications Name=Hadoop Name=Hive Name=Pig --use-default-roles --ec2-attributes KeyName=myKey --instance-type m5.xlarge --instance-count 3```

 
#### What are some benefits to using the cloud?

Agility-easy access to broad range of technologies that you can spin up and deploy in minutes.

Elasticity - the ability to provision resources flexibly and according to peak levels of business activity and spin them down just as quickly.  

Cost savings - trade capital expenses (rent, data centers, physical servers) for variable expenses and only pay for IT as you consume it and take advantage of economies of scale.

Deploy globally in minutes - expand to new geo regions and deploy infrastructure closer proximity to end users to reduce latency and imprve experiences.

#### What is the Spark History Server?

A monitoring tool that displays info about completed Spark applications.  Info is pulled from data that applications by default write to a directory on a HDFS (event logs).    It allows re-creation of the applications web UI from event logs.  An extension of the Apache Spark Web User Interface (UI) that presents a visual interface with detailed information about completed and running Spark jobs on a cluster. You can dive into job-specific metrics, and information about scheduler stages, tasks, and running executors. 

#### What does it mean to “spill to disk” when executing spark tasks?

Spark's operators spill to disk if they don't fit in memory. 

For example, certain shuffle operations consume significant amounts of heap memory since they employ in-memory data structures to organize records before or after transferring them.  When data does not fit in the memory Spark will spill these tables to disk, meaning it will write them to disk.  Then when it needs the data again, it will read it from disk. 

Cached datasets that do not fit also spill to disk or are recomputed depending on the storage level that is set on the RDD.

#### Why can Spark skip entire stages if they are the same between jobs?

When Spark shuffles, it also writes to disk.  When it writes to disk the data can be reused in the future jobs, so Spark will skip stages if the output of a stage already exists on local disk or is cached in memory.

#### What is a reasonable number of partitions for Spark?

Because the level of parallelism is important for fully utilizing a cluster, it depends on the data you have, the transformations you are implementing and overall configuration.  If the number of partitions is too low, you'll have GC pauses, pauses while resources are held up by jobs of different size and memory issues, or even some cores will not be utilized.  If the number is too high, the maintenance (overhead) cost in managing many small tasks and data movement exceeds the processing cost.  Factor 2 or 3 are common for the lower bound and enough partitions to bring completion rates to 100ms as an upper bound.  Another common piece of advice is to err on the side of caution and have too many partitions/tasks and go slower, rather than for the job to fail.

#### When during a Job do we need to pay attention to the number of partitions and adjust if necessary?

This would be the most painful part of any Spark pipeline, the shuffle triggered by wide transformations.  The default `spark.sql.shuffle.partitions` option sets the number of partitions used during shuffles (200 by default) and this can work sub-optimally depending on your data size. Too little data and we may end up with many partitioned files with few records in each partitions.   Too much data and tasks may take a long time to run or we might get out of memory errors.

After a shuffle it might be necessary to repartition your data.  You can set this with `spark.conf.set("spark.sql.shuffle.partitions", 16)`

#### What is spark.driver.memory?  

Amount of memory to use for the driver process (where SparkContext is initialized.  Default 1g, must be set in command line if running in client mode.

#### What about spark.executor.memory?

Amount of memory to use per executor process. Default 1g, default allocated from JVM memory heap.  

#### What are some steps we can take to debug a Spark Application?

In the AWS EMR dashboard we can view a clusters Steps/jobs and take a look at the logs (controller, syslog, stderr, stdout) for application progress, error messages and exit conditions.  We can look for Exception and Error messages.  Following the applications progress by viewing which tasks finished successfully and at which point our app got hung up can give us clues as to which part of the code/logical plan to examine.  

We can further optimize our apps by going into the Spark history server to see what stages were skipped by drilling down into the stages to see shuffle details (read/write), skipped stages, and specific executors to see how much time was spent doing GC, how the tasks were distributed among our executors resources. 

If log aggregation is turned on (yarn.log-aggregation-enable) container logs are copied to HDFS and deletd on the local machine.  These logs can be viewed using `yarn logs -applicationId <app ID>`.  Or viewed in HDFS.

#### What is a Spark Application? Job? Stage? Task?

The main function is the application.  It creates the SparkContext and contains the narrow and wide transformations.  

When an action is taken on an RDD a job is created.  Jobs are a sequence of stages.  Stages are divided by shuffles (triggered by actions) into tasks.  A task is the smallest unit of work.

A stage is a sequence of tasks that can be run together in parallel without a shuffle.  These are performed lazily and can skipped if the computing has already been done previously and cached.

A task is a single operation applied to a partition, each task is executed as a single thread on an executor.  If you have 5 partitions of your data, a map() operation triggers 5 Tasks, one for each partition, taking place on 5 executors.


#### When we cache an RDD, can we use it across Tasks? Stages? Jobs?
A cached RDD is normally shared between stages, but normally not Jobs.  However, if shuffle files are written to local disk, they could be used by future jobs.  


#### What are Persistence Storage Levels in Spark?

##### MEMORY_ONLY Store RDD as deserialized Java objects in the JVM. If the RDD does not fit in memory, some partitions will not be cached and will be recomputed on the fly each time they're needed. This is the default level.

##### MEMORY_AND_DISK Store RDD as deserialized Java objects in the JVM. If the RDD does not fit in memory, store the partitions that don't fit on disk, and read them from there when they're needed.

##### MEMORY_ONLY_SER (JAVA AND SCALA) Store RDD as _serialized_ Java objects (one byte array per partition). This is generally more space-efficient than deserialized objects, especially when using a [fast serializer](https://spark.apache.org/docs/2.2.0/tuning.html), but more CPU-intensive to read.
 
##### MEMORY_AND_DISK_SER (JAVA AND SCALA) Similar to MEMORY_ONLY_SER, but spill partitions that don't fit in memory to disk instead of recomputing them on the fly each time they're needed.

##### DISK_ONLY Store the RDD partitions only on disk.

#####  MEMORY_ONLY_2 - REPLICATE EACH PARTITION ON TWO CLUSTERS
MEMORY_AND_DISK_2, ETC.... Same as the levels above, but replicate each partition on two cluster nodes.  Provides faster fault recovery.  Lost data doesnt need to be recomputed, just read.

#####  OFF_HEAP Similar to MEMORY_ONLY_SER, but store the data in [off-heap memory](https://spark.apache.org/docs/2.2.0/configuration.html#memory-management). This requires off-heap memory to be enabled.

#### Some levels have _SER, what does this mean?

Means that the data is serialized as Java objects (one-byte array per partition), generally more space-efficient, but computationally expensive than deserialized objects.


#### Some levels have _2, what does this mean?

REPLICATE EACH PARTITION ON TWO CLUSTERS MEMORY_AND_DISK_2, ETC....

#### If the storage level for a persist is MEMORY_ONLY and there isn't enough memory, what happens?

They will not be stored, and recomputed on the fly.

#### What is the storage level for .cache()?

The default level is MEMORY_ONLY for RDD, MEMORY_AND_DISK for dataset.  Cache is the default storage level (StorageLevel.MEMORY_ONLY - deserialized objects in memory) Persist allows you to specify the storage level for each persisted RDD.  

--



## Notes

#### Spark Lineages and Physical Execution Plan

The lineage of RDDs shown by .toDebugString() consists of a logical plan for the execution of the RDD.  Spark takes the logical plan and turns it into a physical plan that can actually run on the cluster.  

Physical plan is divided into STAGES.
STAGES divided into TASKS.

Each transformation that requires a shuffle starts in a new stage (and are tasks in that stage).  Transformation that don't require a shuffle are tasks within a stage.

Each partition of input data is one TASK.  A text file split into 4 partitions, will spawn 4 tasks.  Each task operates in its own partition, and passes its output to the next task in the stage.

When we shuffle, we redistribute the values across the cluster and change the partitions.  Each partition output from the shuffle spawns one task, the first task in the new STAGE.


---
#### Spark on YARN

***Two Modes: Cluster mode and Client mode***

 - **Cluster mode:** Driver runs inside ApplicationMaster in Yarn.  Output from driver appears in the container spun up for
   ApplicationMaster by the ApplicationManager.
   
   
- **Client mode:** Runs outside of ApplicationMaster and communicates with an ApplicationMaster. Output from driver will appear on YARN master node, or whatever the driver program is running.

The machines used to execute Spark jobs are called **executors**, in YARN these run as containers.

---

#### AWS

AWS provides VMs and services built on top of them.  Almost everything is built on top of EC2s, which stand for Elastic Compute Cloud and is a virtual server.  

Hadoop clusters are available as EMR (Elastic MapReduce), a preconfigured and managed Hadoop cluster, running on EC2s under the hood.

S3 Simple Storage Service, lets you store objects as Buckets.  You can retrieves them with access keys or make them public.  You have fine-grained control of access and efficiency.  

Elastic - EMR can expand and contract based on amount of processing.  Behavior is configurable.

#### What is a DAG (Directed Acyclic Graph)

A DAG is a mathematical construct that is commonly used in computer science to represent dataflows and their dependencies. DAGs contain vertices, or nodes, and edges. Vertices in a dataflow context are steps in the process flow. Edges in a DAG connect vertices to one another in a directed orientation and in such a way that it is impossible to have circular references
