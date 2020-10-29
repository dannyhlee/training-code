
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
