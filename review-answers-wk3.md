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

Unix is an operating system developed by Bell Labs in the 70s.  Originally it was sold with a license that allowed its source code to be modified.  Later this was amended, but development continued in flavors like BSD and private companies had their own version of Unix variants (like SunOS/Solaris, HP-UX, AIX, Xenix.  

Ubuntu is a unix-like operating system because its built on the Linux kernel and GNU OS and tools. Linux distributions were created to provide free and open source software in light of the UNIX licensing/copyright battles in the early 90s.


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

An absolute (or full) path points to the same location in a file system, regardless of the current working directory.  A relative path takes into account the CWD and can change depending on what directory we are currently in.  A '.' references our current directory.  A '..' references a directory 1 level above (parent directory). 

#### How do permissions work in Unix?

Permissions are divided into read, write and execute permissions.  They are also separated by users and groups.  We can specify permissions for files and directories for owner/group/public.  

#### What are users, what are groups?

Users can be either individual people's accounts or they can be an account for an application to use.  Each recieves a UID.  Some user commands:
```
sudo useradd -m username
sudo passwd username
```
Each user is part of one or more groups.  They can have additional permissions based on their groups.  User and group information is stored in /etc/passwd and /etc/groups.

#### How does the chmod command change file permissions?

We specify the permissions we want to give and the files/directories that we want to modify.  We can see the set permissions with ls -l.

The way this shows up on the filesystem when we use ls is:
```
drwxr-xr-- = directory, r/w/x for owner, r/x for group and r only for public
-r-xr-xr-- = file, r/x for owner and group, r only for public
```
Permissions can be set using the `chmod` command.  0 for no permissions, 4 for read, add 2 for write and 1 for execute.  For example:
```
rwx = 7
rw = 6
rx = 5

rx for owner, group and public would be 555
rwx for owner, and rx for group and public 755

in binary:
rwx r-x r-x would be 755 using the coding above and in binary = 111 101 101 
```

#### What is a package manager? what package manager do we have on Ubuntu?

A package manager takes care of the installation, update and removal of applications.  The ubuntu package manager is apt (Advanced Packaging Tool). 

- update: download package information for all configured sources, it shows package details and availability for installation.

- upgrade: upgrades currently installed packages 

- install, remove, purge, search, show, list

## Day 4

#### What is ssh?

SSH (secure shell) provides an encrypted connection over unsecured networks, by using pairs of cryptographic encryption.  Once logged in, transfers of data and commands can be done securely because all data transferred between SSH server and SSH client is encrypted.

#### Be able to explain the significance of Mapper[LongWritable, Text, Text, IntWritable] and Reducer[Text, IntWritable, Text, IntWritable]

**Mapper**: The 4-tuple [LongWritable, Text, Text, IntWritable] being passed into Mapper specifies the input key-value pair is of type [LongWritable, Text] and the output key-value type is [Text, IntWritable].  

**Reducer**: The 4-tuple Reducer[Text, IntWritable, Text, IntWritable] being passed in represents the types of input and output of the key-value pair.  These are the same for input and output [Text, IntWriteable].

#### What needs to be true about the types contained in the above generics?

They must match outputs to inputs.  The output of mapper needs to match up to input of reducer, or if there is a combiner the output of mapper must line up with the input of combiner, and the output of combiner must line up with the input of the reducer.

#### What are the 3 Vs of big data?

Volume, velocity and variety.  

Volume: Data in large volumes > 1TB
Velocity: Data being generated rapidly (online/server logs)
Variety: Data being in different formats with differing amounts of structure

#### What are some examples of structured data? Unstructured data?

Structured data: SQL database tables, mongo db?  clearly defined data types whose pattern makes them easily searchable.

Semi-structured: XML, csv, email

Unstructured data: formats like audio, video, social media posts, pdf.

#### What is a daemon?

Daemons are computer programs that run as a background process, often forked off and running detached from the invoking session.  They are often long-running and perform specific functions or system tasks.  In keeping with Unix/Linux philosophy of modularity, daemons are programs rather than parts of the kernal.  Many start at boot time and run as long as the system is running.

#### What is data locality and why is it important?

Data locality in MapReduce/Hadoop is a strategy developed to overcome the drawback of cross-switch networking transfer of huge volumes of data.  The different categories of Data Locality in Hadoop are:
- Data local data locality - data located in the same node as the mapper
- Intra-Rack data locality - data is in a different node, but on the same rack
- Inter-rack data locality - data is on a different node on a different rack

#### How many blocks will a 200MB file be stored in in HDFS, if we assume default HDFS block size for Hadoop v2+?

Hadoop v2+ default block size is 128M MB so a 200 MB file will be stored on 2 blocks.

block 1: 128 MB
block 2: 72 MB

#### What is the default number of replications for each block?

The default number of replications is 3.  This is called the replication factor and is stored by the NameNode.  

Blocksize and replication factor are configurable per file.

#### How are these replications typically distributed across the cluster? What is rack awareness?

The HDFS placement policy is to put one replica on one node in the local rack, another on a none in a different (remote rack) and the last on a different node, in the same remote rack.

#### What is the job of the NameNode? What about the DataNode?

NameNode: This is the master.  There is only one or very few per cluster.  The NN keeps the image (FSImage) of the DFS, it knows the names and directories, where to find the contents in the cluster but nothing about the data.  It records edits to the filesystem on the EditLog.  

DataNode: This is the worker.  One per machine in a typical deployment.  The DN keeps actual data and communicates its status to NN (heartbeat) and a Blockreport (list of all blocks on the DN).  Doesnt know anything about the files.

#### How many NameNodes exist on a cluster?

One or few. There can be a secondary NN that backups NN metadata.  Secondary can't step in.  Standby NN can step in.

#### How are DataNodes fault tolerant?

DataNodes' fault tolerance is handled by the NN.  If a DN stops sending heartbeats to the NN, the NN will not make IO requests to them and if any of the blocks that were stored on the node fall below their replication factor, the NN will start a replication process for the data on the DN.

#### How does a Standby NameNode make the NameNode fault tolerant?

Prior to Hadoop 2, the NN was a single point of failure (SPOF) in an HDFS cluster.  The entire cluster would go down until the NameNode was restarted or brought up on another machine.  This affected availability in cases of machine failure, but also for maintenance and sw/hw upgrades.

In a HA (high availability) cluster, 2 or more machines are configured as NameNodes.  One as Active, one as Standby.  The machines share a networked storage device where the Active node durably logs a record of edits, the Standby(s) continually monitor and update their own namespaces to match this log. 

In case of failure, the Standby finishes all writes that are recorded on the shared drive, before a failover occurs.

Standby nodes also receive blockreports and heartbeats to all Standbys.

#### What purpose does a Secondary NameNode serve?

The Secondary helps the primary NameNode to keep its **Fsimage** file and **Edits** log file up to date.  The Fsimage is like a save point in a video game, it has the file system status up to a certain point.  The Edits log file is a list of the changes made since then.  By applying the edits log file transactions to the Fsimage, we can get the current status of the filesystem.  This is what the Primary NameNode will do when it restarts.

However, because many transactions could have occurred between restarts, this can cause problems with filesize of the Edits log and the time to apply all the changes.  The secondary steps in here, by occassionally taking a copy of the Fsimage, applying the edits and then sending it back to the Primary, along with refreshing the edits log to let the Namenode what updates it made.  This keeps the log size manageable and the Fsimage file better updated so restarts can be faster.

#### How might we scale a HDFS cluster past a few thousand machines?

In Hadoop HDFS, the NameNode stores metadata for every file and block in the file system.  In very large clusters with many files, the requirements of memory for storing metadata for each file and block is limiting.  The single NameNode architecture becomes a bottleneck.

HDFS Federation feature in Hadoop 2.0 allows clusters to scale by adding more NameNodes.

#### In a typical Hadoop cluster, what's the relationship between HDFS data nodes and YARN node managers?

They work in tandem, alongside one another in the same machines, but they aren't directly related.  The HDFS data nodes correspond with the NameNode and the Yarn node managers with the Resource Manager.

## Day 5

#### When does the combine phase run, and where does each combine task run?

The combine process is optional, but if configured.  The combine phase runs after the map task is completed and takes place on the mapper server.

#### Know the input and output of the shuffle + sort phase.

The shuffle phase transfers the map output to a reducer.  The sort phase covers the merging and softing of map outputs.  Data is grouped by key and split among the reducers, sorted by the key.  Each reducer obtains all values associated with the same key.  This is the point where large amounts of data will be transfered by network IO.  

#### What does the NodeManager do?

The NodeManager is a per-machine framework agent who is reponsible for creating, monitoring and killing containers at the direction of the ResourceManager (registers and sends heartbeats to RM).  The NodeManager monitors their resource usage (cpu, memory, disk, network) and reporting the same to the Resource manager/Scheduler.  Application masters will request assigned containers and NodeManager creates and starts it.

#### What about the ResourceManager?

The RM has two components, the Scheduler and ApplicationsManager.  The RM arbitrates resources among all the applications in the system.  

#### Which responsibilities does the Scheduler have?

The Scheduler is responsible for allocating resources to the various running applications, subject to capacity, queues, etc.  The Scheduler only handles scheduling and does not monitor or track application statuses.  Does not offer fault-tolerance and doesn't restart tasks on its own.

#### What about the ApplicationsManager?

The ApplicationsManager is responsible for accepting job-submissions, negotiating the first container for executing the ApplicationMaster and provides the service for restarting the ApplicationMaster container in case of failure.

#### What is an ApplicationMaster? How many of them are there per job?

The ApplicationMaster handles making requests to negotiate appropriate resource containers from the Scheduler.  Once it is assigned a container, it requests it from the Nodemaster and tracks their status and monitors progress of tasks, in conjunction with the NodeMaster.  There is one ApplicationMaster per application.  An application is either a single job or a DAG of jobs.

#### What is a Container in YARN?

A container is an abstract notion of a collection of physical resources on the computer.  Such as RAM, CPU cores, disks, network, etc.

#### How do we interact with the distributed filesystem?

We can run filesystem commands using the `bin/hdfs` script.  Many of the commands are the same that we would run on our local filesystem, except we add a `bin/hdfs` and hyphen ('-') in front of the command.

For example:
```
// copy
$ /bin/hdfs -cp /user/hadoop/file1 /user/hadoop/file2  

// list files
$ /bin/hdfs dfs -ls
```

#### What do the following commands do?

- hdfs dfs -get /user/adam/myfile ~

This command will copy the remote file named `myfile` in the directory `/user/adam` to my user's home directory on my local filesystem

- hdfs dfs -put ~/coolfile /user/adam/

This command will put my local file `coolfile` located in my home directory into the remote HDFS directory `/user/adam`

