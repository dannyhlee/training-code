

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
#### How can we see the Lineage?
#### What do the indentations mean in the printed lineage?
#### What is the logical plan?  The physical plan?
#### How many partitions does a single task work on?
#### What’s the difference between cluster mode and client mode on YARN?
#### What is an executor?  What are executors when we run Spark on YARN?
#### What is AWS?
#### EC2?
#### S3?
#### EMR?
#### What does it mean to run an EMR Step Execution?
#### What are some benefits to using the cloud?
#### What is the Spark History Server?
#### What does it mean to “spill to disk” when executing spark tasks?
#### Why can Spark skip entire stages if they are the same between jobs?
#### What is a reasonable number of partitions for Spark?
#### When during a Job do we need to pay attention to the number of partitions and adjust if necessary?
#### What is spark.driver.memory?  What about spark.executor.memory?
#### What are some steps we can take to debug a Spark Application?

#### What is a Spark Application? Job? Stage? Task?
#### When we cache an RDD, can we use it across Tasks? Stages? Jobs?
  - NOTE: Adam had this question wrong in Wed notes! it's fixed now
#### What are Persistence Storage Levels in Spark?
#### Some levels have _SER, what does this mean?
#### Some levels have _2, what does this mean?
#### If the storage level for a persist is MEMORY_ONLY and there isn't enough memory, what happens?
#### What is the storage level for .cache()?
