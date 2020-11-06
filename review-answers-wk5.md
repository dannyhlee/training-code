


## Notes

#### Spark Lineages and Physical Execution Plan

The lineage of RDDS shown by .toDebugString() consists of logical plan for the execution of the RDD.  Spark takes the logical plan and turns it into a physical plan that can actually run on the cluster.  

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

---

#### What is the lineage of an RDD?

The lineage of an RDD is a graph all the parent RDDs to this RDD.  It is the path of transformation as a logical execution plan.   Aka RDD operator graph or RDD dependency graph.

#### How can we see the Lineage?

We can view the lineage using .toDebugString or the explain call.  
https://developer.ibm.com/technologies/artificial-intelligence/blogs/how-to-understanddebug-your-spark-application-using-explain/

When we read the lineage it should be from bottom up.


#### What do the indentations mean in the printed lineage?

The indentations indicate a shuffle boundary/new stage.  The number in round brackets show the level of parallelism at this stage.

#### What is the logical plan?  The physical plan?

A logical plan describes what needs to be done without deciding how to do it, a physical plan describes what every node would do.  The physical plan is divided into stages, stages contain tasks.

#### How many partitions does a single task work on?

Each partition of the input data corresponds to one task.

#### What’s the difference between cluster mode and client mode on YARN?

In Cluster mode spark runs inside an ApplicationMaster in Yarn, output from our driver will appear inside the Yarn container created by ApplicationMaster by the ApplicationManager.  Cluster manager - An external service for acquiring resources on the cluster (e.g. standalone manager, Mesos, YARN).

In client mode, the driver runs outside of YARN (often on YARN's master node) and communicates with ApplicationMaster.  Output appears in its current environment (often Yarn's master node).

#### What is an executor?  What are executors when we run Spark on YARN?

An executor run the Spark jobs and in Yarn run as containers.    
A process launched for an application on a worker node, that runs tasks and keeps data in memory or disk storage across them. Each application has its own executors.  Spark acquires executors on nodes in the cluster, which run computations and store data for your application.  Spark sends application code (Jar or Phython files passed to SparkContext) to the executors.  Then Spark sends tasks to the executors to run.

#### What is AWS?

AWS provides virtual machines and services built on top of them.  

#### EC2?
#### S3?
#### EMR?

[Amazon Elastic MapReduce](https://aws.amazon.com/emr/) (EMR) is a fully managed Hadoop and Spark platform from Amazon Web Service (AWS). With EMR, AWS customers can quickly spin up multi-node Hadoop clusters to process big data workloads.

#### What does it mean to run an EMR Step Execution?

-   An EMR cluster can be run in two ways. When the cluster is set up to run like any other Hadoop system, it will remain idle when no job is running. The other mode is for “step execution.” This is where the cluster is created, runs one or more steps of a submitted job, and then terminates. Obviously the second mode of operation saves costs, but it also means data within the cluster is not persisted when the job finishes. This is where EMRFS becomes important.
- 
#### What are some benefits to using the cloud?

Agility-easy access to broad range of technologies that you can spin up and deploy in minutes.

Elasticity - the ability to provision resources flexibly and according to peak levels of business activity and spin them down just as quickly.  

Cost savings - trade capital expenses (rent, data centers, physical servers) for variable expenses and only pay for IT as you consume it and take advantage of economies of scale.

Deploy globally in minutes - expand to new geo regions and deploy infrastructure closer proximity to end users to reduce latency and imprve experiences.

#### What is the Spark History Server?

A monitoring tool that displays info about completed Spark applications.  Info is pulled from data that applications by default write to a directory on a HDFS (event logs).    It allows recreation of the applications web UI from event logs.  An extension of the Apache Spark Web User Interface (UI) that presents a visual interface with detailed information about completed and running Spark jobs on a cluster. You can dive into job-specific metrics, and information about scheduler stages, tasks, and running executors. 

#### What does it mean to “spill to disk” when executing spark tasks?
#### Why can Spark skip entire stages if they are the same between jobs?


#### What is a reasonable number of partitions for Spark?


#### When during a Job do we need to pay attention to the number of partitions and adjust if necessary?

#### What is spark.driver.memory?  

Amount of memory to use for the driver process (where SparkContext is initialized.  Default 1g, must be set in command line if running in client mode.

#### What about spark.executor.memory?

Amount of memory to use per executor process. Default 1g, default allocated from JVM memory heap.  

#### What are some steps we can take to debug a Spark Application?

#### What is a Spark Application? Job? Stage? Task?

#### When we cache an RDD, can we use it across Tasks? Stages? Jobs?
  - NOTE: Adam had this question wrong in Wed notes! it's fixed now
  - 
#### What are Persistence Storage Levels in Spark?

MEMORY_ONLY Store RDD as deserialized Java objects in the JVM. If the RDD does not fit in memory, some partitions will not be cached and will be recomputed on the fly each time they're needed. This is the default level.
MEMORY_AND_DISK Store RDD as deserialized Java objects in the JVM. If the RDD does not fit in memory, store the partitions that don't fit on disk, and read them from there when they're needed.
MEMORY_ONLY_SER (JAVA AND SCALA) Store RDD as _serialized_ Java objects (one byte array per partition). This is generally more space-efficient than deserialized objects, especially when using a [fast serializer](https://spark.apache.org/docs/2.2.0/tuning.html), but more CPU-intensive to read.
MEMORY_AND_DISK_SER (JAVA AND SCALA) Similar to MEMORY_ONLY_SER, but spill partitions that don't fit in memory to disk instead of recomputing them on the fly each time they're needed.
DISK_ONLY Store the RDD partitions only on disk.
MEMORY_ONLY_2 - REPLICATE EACH PARTITION ON TWO CLUSTERS
MEMORY_AND_DISK_2, ETC.... Same as the levels above, but replicate each partition on two cluster nodes.  Provides faster fault recovery.  Lost data doesnt need to be recomputed, just read.
OFF_HEAP Similar to MEMORY_ONLY_SER, but store the data in [off-heap memory](https://spark.apache.org/docs/2.2.0/configuration.html#memory-management). This requires off-heap memory to be enabled.

#### Some levels have _SER, what does this mean?

Means that the data is serialized as Java objects (one-byte array per partition), generally more space-efficient, but computationally expensive than deserialized objects.


#### Some levels have _2, what does this mean?

REPLICATE EACH PARTITION ON TWO CLUSTERS MEMORY_AND_DISK_2, ETC....

#### If the storage level for a persist is MEMORY_ONLY and there isn't enough memory, what happens?

They will not be stored, and recomputed on the fly.

#### What is the storage level for .cache()?

The default level is MEMORY_ONLY for RDD, MEMORY_AND_DISK for dataset.  Cache is the default storage level (StorageLevel.MEMORY_ONLY - deserialized objects in memory) Persist allows you to specify the storage level for each persisted RDD.  
