## Day 1 
### MapReduce Whitepaper

#### What does the Map part of MapReduce take in? What does it output? (1)

#### What about the Reduce part of MapReduce? (1)

map (k1, v1) -> list (k2, v2) 
reduce (k2, list(v2)) -> list (v2)

#### What is the optional Combiner step? (1)

A local reduce done at the end of the map phase to reduce complexity, right before the intermediate files are written to disk.

#### What is GFS? (2)

The Google file system, a proprietary distributed file system.  A master node with 

#### How many replications of data does GFS provide by default? Block size? (2)

64mb is default block size.

#### HDFS, Hadoop Distributed FileSystem, is the same by default

#### Why is the Combiner step useful in the case of a wordcount? (2)

In case of word count chances are almost definite that there will be large number of the same word - zipthe distribution.

#### Is the Master fault tolerant? Why or why not? (3)

The master could or couldnt be.  GFS allows for shadow masters, but the chances of a master failing is lower.  But it isn't as fault tolerant of workers.  

#### Are the workers fault tolerant? Why or why not? (3)

Workers fail a lot more often.  In any event, the worker will restart.

#### What happens to the output of completed Map tasks on failed worker nodes? (3)

They are ignored.

#### What is Data Locality? Why is it important? (4)

Data stored on local machine to reduce network traffic.  

#### How does MapReduce increase processing speed when some machines in the cluster are running slowly but don't fail? (4)

If there are laggards, then the master will start up other instances to dupliucate the processing and whichever finishes first will b used.

#### What does a custom partitioning function change about how your MapReduce job runs? (4)

There is a default partitioning function, custom partitions let you specifiyu the way it is broken up.

#### What is a hashcode? How are hashcodes used in (default) partitions? (5)

The hash function generates a u

#### What does it mean that side effects should be atomic and idempotent? (5)

idempotent results in the same results

#### What are Counters for? (5)

Counters count the number of specific tasks

#### Where do Map tasks read from? Write to? (6)


#### Where do Reduce tasks read from? Write to? (6)


#### Which of the above I/O steps would you expect to take the longest?(6)


#### Walk thorugh a MapReduce job that counts words in the sentence : "the quick brown fox jumped over the lazy dog" (6)


#### How does this work for 2 input blocks (so 2 Map tasks) and 1 reduce task? What if we had 2 Reduce tasks?
