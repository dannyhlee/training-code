## Day 1 
### MapReduce Whitepaper

#### What does the Map part of MapReduce take in? What does it output? (1)

It takes in the input files, split up into M pieces of typically 16 mb to 64 mb per piece, which is user-definable.  It outputs a **list** of intermediate keys and values which been generated from passing the inputted  key/value pairs to a user-defined Map function.

#### What about the Reduce part of MapReduce? (1)

It takes in buffered data from the local disks of the map workers, this data is made up of the intermediate key and value pairs, which the Map part has produced.  It then merges these values together to form a possibly smaller set of values.

map (k1, v1) -> list (k2, v2) (output of map)
reduce (k2, list(v2)) -> list (v2) (reduced to zero or one output value)

#### What is the optional Combiner step? (1)

A local reduce done at the end of the map phase to reduce complexity, right before the intermediate files are written to disk.

#### What is GFS? (2)

The Google file system, a proprietary distributed file system.  It has one master node, and multiple chunk servers. Chunk servers store fixed-size chunk of data is given a 64bit label by the master node. 

#### How many replications of data does GFS provide by default? Block size? (2)

64mb is default block size.  Each chunk is replicated, by default 3 times, but frequently accessed files may be duplicated more.

#### HDFS, Hadoop Distributed FileSystem, is the same by default

#### Why is the Combiner step useful in the case of a wordcount? (2)

Sometimes there's is significant repeition in the intermediate keys produced by the map task, like in word counting where <the, 1> will be repeatedly produced.  By performing a "reduce" function to partially merge these instances within specific machines before sending them to be saved to the intermediate file, significant network bandwidth savings can be had.

#### Is the Master fault tolerant? Why or why not? (3)

The master could or couldnt be.  GFS allows for shadow masters, but the chances of a master failing is lower.  But it isn't as fault tolerant of workers.  According to the whitepaper, if the master fails, the computation will abort.

#### Are the workers fault tolerant? Why or why not? (3)

Having been built on many commodity machiunes, workers fail a lot more often.  So, they are built to be fault tolerant.  Any map or reduce tasks that is in progress on a failed worker is reset and rescheduled by the master.  MapReduce is resilient to large-scale worker failures.

#### What happens to the output of completed Map tasks on failed worker nodes? (3)

The data is discarded as a workers output is stored on the failed machine so is inaccessible.  

#### What is Data Locality? Why is it important? (4)

Data locality is the strategy of taking data proximity into account when scheduling tasks.  By bringing the task to the data, the need to transfer data over the network reduces the inherent latency of network data transfer.  If not the same machine, the master will look for the same network, moving up the chain until it finds the closest replica of the data.  

#### How does MapReduce increase processing speed when some machines in the cluster are running slowly but don't fail? (4)

If there are laggards, then the master will start up other instances to dupliucate the processing and whichever finishes first will b used.

#### What does a custom partitioning function change about how your MapReduce job runs? (4)

There is a default partitioning function, custom partitions let you specify the way it is broken up either by number of Reduce tasks/output files or other logically organized fashion.

#### What is a hashcode? How are hashcodes used in (default) partitions? (5)

A hashcode is used calculate a value upon which data is divided into partitions.  The default parititioning function is hash(key) mod R, which takes calculated hash of (key) and takes the remainder of the division by the number of Reduce tasks/output files desired.

#### What does it mean that side effects should be atomic and idempotent? (5)

Idempotent is a property applied to operations which can be applied multiple times with the same results.  Atomic side effects shouldnt affect other operations.

#### What are Counters for? (5)

The MapReduce library provides a way to count occurances of various events.  We can track how often something happens in the processing of data.  The master aggregates the counter values from different machines and returns them to the user when the operation is completed.  They are also available on the master statuys  page.

#### Where do Map tasks read from? Write to? (6)

Map tasks read from the input files and after mapping the files, saves them locally as Intermediate files.

#### Where do Reduce tasks read from? Write to? (6)

Reduce tasks read from the Intermediate files and write to the output files.

#### Which of the above I/O steps would you expect to take the longest?(6)

Network transfer would take the longest in terms of I/O, because computer memory/local disk access is fast, but transfering over a network is much slower in comparision.

#### Walk thorugh a MapReduce job that counts words in the sentence : "the quick brown fox jumped over the lazy dog" (6)



#### How does this work for 2 input blocks (so 2 Map tasks) and 1 reduce task? What if we had 2 Reduce tasks?


## Day 3

#### What was the "Hadoop Explosion"?

The Hadoop explosion was a flurry of innovation that followed the development of Hadoop.  Many specific tools were created to take advantage of map reduce.  The Hadoop framework for processing huge volumes of a wider variety of data created a new way to deal with the huge amounts of data being generated.  

#### What about CDH?

The Cloudera Distribution Hadoop is an Apache Hadoop distribution provided by Cloudera Inc.  Its a complete, tested and widely deployed distribution, 100% open source and offers batch processing, interactive SQL and interactive search as well as enterprise-grade continuous availability.  

Parts of CDH:
- Apache Hadoop: reliable, scalable distributed storage and computing
- Apache Accumulo: A secure, distributed data store to serve performance-intensive Big Data applications
- Apache Flume: For collection and aggregating log and event data and real-time streaming it into Hadoop.
- Apache HBase: Scalable record and table storage with real-time read/write access
(to be continued... https://www.cloudera.com/products/open-source/apache-hadoop/key-cdh-components.html )

#### What are some differences between hard disk space and RAM?

RAM is short term memory, where things can be quickly stored and retrieved, however it is temporary and will be erased as soon as our computer is shut down.  Disk space takes longer to read and write to, but the storage is long-term and can persist even after a machine's power is turend off.

#### What is a VM? (short)

Virtual Machine.

#### What is AWS? (short)

Amazon Web Services

#### What is/was Unix? Why is Ubuntu a Unix-like operating system?




#### Know basic file manipulation and navigation commands in Unix:

ls -al: list ALL files in the directory in LONG format.  This shows hidden files and directories, as well as permissions, user/group ownership, byte size, date of creation and name.
cd: change directory
pwd: print working directory.  It shows the directory you are currently in.
mkdir: creates a directory
touch: creates a 0-byte file.
nano: a simple text editor
man: man brings up manual pages for a given command
less: reads content of a file and prints to screen in a paginated manner
cat: prints content to a screen without pagination
mv: move a file from one location to another, can also rename files and directories
cp: copy a file from one location to another
rm: removes a file from the filesystem.  -r to remove recursively.
history

#### What's the difference between an absolute and a relative path?



#### How do permissions work in Unix?

#### What are users, what are groups?

#### How does the chmod command change file permissions?

#### What is a package manager? what package manager do we have on Ubuntu?

## Day 4

#### What is ssh?

Having secure communication over an insecure network.  Using a key-pair, where you have a public and private key.  We can access a remote machine as if we had a shell.

#### Be able to explain the significance of Mapper[LongWritable, Text, Text, IntWritable] and Reducer[Text, IntWritable, Text, IntWritable]
#### What needs to be true about the types contained in the above generics?
#### What are the 3 Vs of big data?
#### What are some examples of structured data? Unstructured data?
#### What is a daemon?
#### What is data locality and why is it important?

Data locality in MapReduce/Hadoop is a strategy developed to overcome the drawback of cross-switch networking transfer of huge volumes of data.  The different categories of Data Locality in Hadoop are:
- Data local data locality - data located in the same node as the mapper
- Intra-Rack data locality - data is in a different node, but on the same rack
- Inter-rack data locality - data is on a different node on a different rack

#### How many blocks will a 200MB file be stored in in HDFS, if we assume default HDFS block size for Hadoop v2+?
#### What is the default number of replications for each block?
#### How are these replications typically distributed across the cluster? What is rack awareness?
#### What is the job of the NameNode? What about the DataNode?
#### How many NameNodes exist on a cluster?
#### How are DataNodes fault tolerant?
#### How does a Standby NameNode make the NameNode fault tolerant?
#### What purpose does a Secondary NameNode serve?
#### How might we scale a HDFS cluster past a few thousand machines?
#### In a typical Hadoop cluster, what's the relationship between HDFS data nodes and YARN node managers?


## Day 5

When does the combine phase run, and where does each combine task run?

Know the input and output of the shuffle + sort phase.

What does the NodeManager do?

What about the ResourceManager?

Which responsibilities does the Scheduler have?
What about the ApplicationsManager?
What is an ApplicationMaster? How many of them are there per job?

What is a Container in YARN?

How do we interact with the distributed filesystem?

What do the following commands do?

hdfs dfs -get /user/adam/myfile ~
hdfs dfs -put ~/coolfile /user/adam/

