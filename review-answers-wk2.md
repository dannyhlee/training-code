
## Day 3

#### How do we specify dependencies using sbt?

Project dependencies can be specified by concatenating them to the `libraryDependencies` value member of the Keys object in sbt.  This can be done in the file build.sbt, located in our project's root directory.  The format is:
```
libraryDependencies += organization %% name % version
libraryDependencies += groupID % artifactID % revision
libraryDependencies += groupID % artifactID % revision % configuration

// examples:

// equivalent assuming project's Scala version is 2.11
libraryDependencies += "org.scala-stm" % "scala-stm_2.11" % "0.8"
libraryDependencies += "org.scala-stm" %% "scala-stm" % "0.8"

```
The single percent  (%) symbol is a method used to build dependencies (technically, [creating ModuleID objects from strings](https://www.scala-sbt.org/release/docs/Library-Dependencies.html)) . Using double percent (%%) after the groupID inject your project's Scala version and appending it to the artifact name. This is useful in the case your Scala version is changed, regardless, sbt will retrieve the right version.  

#### Why do we use databases instead of just writing to file?

Database add structural organization to data in the form of entities and relationships.  We are able use these to create complex queries and more efficiently store, access and backup data.  We improve data integrity by reducing updating errors.  We provide security by enacting access permissions on data and only showing what we want through views.  We provide a controlled method of concurrent access and crash recovery.

#### What is a port number?

A port number is a 16-bit unsigned integer (0 to 65535) that identifies a communication endpoint on a server.  When a client makes a request to a server it attempts to address a specific virtual port.  Ports are software based and managed by the server OS.  Each port is associated to a specific process or service.  For example, HTTP protocol goes to port 80, FTP to 20 and 21 (21 to connect hosts, 20 to transfer data), SSH port 22, SMTP 25, HTTPS 443, RDP 3389.

#### What's the default port for MongoDB?

The default port is 27017.

#### What is a database?

A database is an organized collection of structured data stored electronically.  It is made up of entities (models of something) and relationships (between models).  An entity has attributes to store data specific to that entity.  Using these concepts we can structure data in a way that makes it accessible using queries that logically collect parts of the database that fit the criteria and return them.

#### What is a collection?

In MongoDB, a collection is part of a database, and there can be many collections in a single database.  A collection is made up of documents, and is analogous to RDBMS tables.  They are entities that organize documents into some kind of logical collection.  Though there are aren't enforced rules (or schema) that dictates how these collections are organized, logic dictates that they collect documents in some sort of organized fashion.

#### What is a document?

A document is container which stores data in key-value pairs.  The format they use, BSON, is similar to JSON, but instead binary and includes additional types that aren't available in JSON.  These fields can hold all sorts of data including simple types (int, char, str), data structures (lists, arrays, sets) and embedded sub-documents.  This style of embedding documents within documents is generally referred to as "denormalized".

#### What rules does Mongo enforce about the structure of documents inside a collection?

Mongo does not enforce a strict structure on the types of data, or the way in which data is stored.  Different strategies will provide read speed or update speed and these factors must be taken into account when deciding on a Data modelling strategy.  Embedding provides better read performance, as well as the ability to request and retrieve related data in a single operation.  It also provides a way to updated all related data in a single atomic write operation.  However, there is a limited document size and depth, currently BSON's maximum data size is 16 mb and 100 layers of nesting.

Normalized data models are used when duplication doesn't provide enough read performance, compared to the implications of duplication.  And also, when its necessary to represent complex m-to-m relationships or modelling large hierarchical data sets.

#### What is JSON?

JSON stands for JavaScript Object Notation and is a lightweight data-transporting format.  Easy to read and write, its commonly used on the internet to transmit data in a structured fashion between server and client.   There's 

Structurally, the data is written as name/value pairs and separated with a colon.  All fields are enclosed with double quotes.  An object is enclosed with curly braces, while arrays are enclosed with square brackets.

#### What are JSON data types?

JSON contains Objects (name-value pairs, where the name is a key and the values can be made up of any JSON data type including other objects and arrays.  Arrays, or ordered lists of zero or more values, each which can be of any type.  Boolean (true, false), String, Number.

#### What is BSON?

BSON is Binary JSON, a binary format used for representing data structures, including associate arrays (aka name-value pairs).  One design goal of BSON was to speed up traversal of documents, so it includes indexing data to its document as well as storing numbers in their native format, bypassing the need to parse them from String.  

#### What are some of the data types included in BSON?

Along with String, BSON stores its numbers in native format (32/62 bit Integer, Double for floating point values, Boolean, Arrays, Objects, Null, Timestamp, Date, Md5 Binary Data, ObjectID and RegExp.

#### What is an ObjectId?

The ObjectId a BSON type that is the default data type for the _id field that exists (and is automatically  indexed) in every MongoDB document.  Its a (likely) unique 12-byte combination that acts as the primary key in a collection, and includes a timestamp we can access with ObjectId.getTimestamp().

#### What is the _id field for in mongo?

This field exists in every MDB document and is automatically indexed by MongoDB.  Architecturally, by default, _id is of the BSON type ObjectID, but this can be overriden at document creation.  After creation, the _id is immutable.  

#### What does find() do?

The find() method is used to select and return documents in a collection.  Its called on the collection with:
```
db.collection.find(query, projection)
```
With empty clamshells, it will return all documents in the collection.  We can add query parameters to find particular documents, and projections to specify which fields from those returned documents to return.  Along with find() there are five other methods for fetching records:
- findAndModify()
- findOne()
- findOneAndDelete()
- findOneAndReplace()
- findOneAndUpdate()

#### What is a filter in a mongodb query?

I'm guessing you mean filtering using [Query Selectors](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors), in this case, a filter is way to selectively return documents from a MongoDB collection using query selectors to define selection criteria.  Instead of getting the whole collection and working on the results from Scala's side, we ask MongoDB to do the filtering for us and just give us the documents we need.

#### What are some examples of filters?
```
db.collection.find({ 
	title: { $eq: "scala comic" }
}) // find the comics that are titled "scala comic"

db.comics.find({ 
	title: { $regex: /borg/i } 
})	// find comics that match regular expression 'borg' (case insensitive).

db.collection.find( {
	color: "YELLOW",
	$or: [ { quantity: { $lt: 10 } }, { name: /^bana/ } ]
}) 	// find items that are "YELLOW" **and** either less than 
	// 10 quantity or whose name begins with "bana"
```

#### What do sort and limit do?

We can chain the .sort() method to our find() and it will sort the returned records.  Order 1 and -1 correspond to ascending and descending order.  Defaulting to ascending order. For example:
```
db.studentdata.find({}, {
	"student_id": 1, _id:0
}).sort({
	"student_id": -1
})  // find all students, add projection which shows student_id but hides _id.  Then sort on student_id in descending order.
```
**.limit(i)** - limits the number of records we want to display or return to **i**
**.skip(i)**  - skips **i** records, before taking from the collection.

#### What is a projection in a mongodb query?

By default MongoDB returns all fields of matching documents returned from a find().  To limit which fields are returned by MongoDB we use projections to specify which fields to return.   We enclose a list of fields from the returned document and indicate with a 1 or 0 whether we do or do not want the value to be returned.  

```
db.studentdata.find({}, { _id: 0 }) })
// return all documents from studentdata, but remove the _id field.
```

## Day 4

#### What is multiplicity? Examples of 1-to-1, 1-to-N, N-to-N?

With the realm of database system and data modelling, specifically UML,  the multiplicity attribute of a relationship specifics the cardinality (or number of instances) of an entityType to instances of another entityType.  Some multiplicities are:
- 1 to 1 ( A user to their configuration file)
- 1 to N (or many) (a celebrity to their fans)
- Many to Many (students and courses)

#### What is cardinality?

Is the measure of the number of elements in a set, basically how many elements of a set.  Cardinalities are a term used in ER models (Entity relationship model) to relate the minimum and maximum cardinality between two related entities.  Some ratios are:
- m:n - many to many
- m:1 - many to one
- 1:n - one to many
- 1:1 - one to one

#### What are some advantages of handling document relationships by embedding documents?

Having all the related data in one place and available through one query can be advantageous.  

Some advantages of embedding related documents within one another is that reduce the need for performing joins on normalized data.  Normalization reduces redundancy, which facilitates updates, but when we need to read data it means pulling data from different parts of the hard drive.  In reading  a row of data 99% of the time is taken to seek to the location.  Reading data adjacent to the location is fast.  

So, embedding documents provides locality, so once the document is located on the disk, reading all of its data is a fast operation because the data is adjacent to one another.  

Another advantage of embedding is Atomicity and Isolation in writing data.  In relational databases updates are done as transactions which are guaranteed Atomicity.  MongoDB is designed without multi-document transactions (although this functionality has been added in MongoDB 4.0).  


#### Disadvantages of the same?

The flip side of the coin is having all the data in one document, may mean you have too much data.  So, our queries are returning a lot of data that isn't necessary all the time. 

There is a 16mb limit to the size of documents, larger documents use more ram and disk space.  Ram is a critical resource and you have relationships of one-to-many, wher ethe many can be of very high or unpredictable arity can mean that "viral" requests for articles or photos can consume too many resources.

Another example is an article with 1000 comments, you might not want to query all the comments, just a portion of them, before asking for more if the client requests it. 

A lot of data will come pre-joined that dont need to be joined and could cause problems in high-arity relationships.

#### What about handling document relationships using references -- advantages and disadvantages?

Having references to related data is advantageous in that it allows a strategic structure to minimize the duplication of data.  This comes in handy when all data is not needed all the time.  Less requested data can be set in a separate document or collection. 

It helps with document size management, reducing the size of individual documents.  Reduces the size of requests, although it increases the number of requests.

A disadvantage is that updates are not atomic and although transactions have been introduced, by default we can't update all documents and related references atomically which can lead to data inconsistency.

#### What is an Index?

In MongoDb an index is a data structure that stores a part of a collections data set in an easy to traverse form.  There are different kinds of indexes for different types of data:  
- Single field - _id field is one.  Ascending or descending sorted.
- Compound index - Indexes on multiple fields.  Sorting first by one then the other.
- Multikey indexes - index content in arrays, entries are made for each element of the array.
- Geospatial index - for geospatial coordinate data
- Text indexes - text indexes for searching string content.
- Hashed indexes - for hash based sharding.  

It's like an index in a book and allows us to more quickly search through a collection for the document(s) we are looking for.  MongoDB indexes the _id field automatically, but we can other indexes on document fields.  

#### What advantages does creating an Index give us? Disadvantages?

Indexes speed up queries for that field, but slows down updates to the document, because changes must also be marked in the index.

Without an index MongoDB does a collection scan and scans every document in  a collection to select query-matching documents.


#### What is CRUD?

CRUD is an acronym that stands for:
- Create - creating new data
- Read/Retrieve - reading data in the db
- Update - updating data
- Delete - deleting records

The term is used to generalize database operations and is also used very often with APIs (especially RESTful ones).  

#### Some example CRUD methods for Mongo? (The Scala methods mostly match mongo shell syntax)

- Create - insertOne(), insertMany()
- Read - find()
- Update - UpdateOne(), UpdateMany(), replaceOne()
- Delete - deleteOne(), deleteMany()

#### What is a distributed application? A distributed data store?

A distributed application operates on more than one physical or virtual machine at the same time, with a network connection between them.  An example is an application with has a client front end that requests data from a server where data is stored.  It could include multiple clients and/or multiple servers.

A distributed data store is infrastructure that can split data across multiple physical servers and across multiple data centers.  It typically takes the form of a cluster of storage units, with a mechanism for data synchronization and coordination between cluster nodes.  (Ex: Amazon S3, MS Azure)

DDS provide redundancy and scalability, by providing the ability to spin up new instances if one goes down or if more capacity is required.

#### What is High Availability? How is it achieved in Mongo?

High availability is a characteristic or property of a system to almost always be available and avoiding downtime.   By having high fault tolerance the system is able to experience faults and continue functioning (albeit with degraded functionality).  One way to provide redundancy is through failover behaviors such as MongoDB's replica sets.  A replica set is at least 3 instances of a database running in a distributed manner.  If the primary fails, a replica will take over and with services like Amazon S3 new instances can be started up.

#### What is Scalability? How is it achieved in Mongo?

Scalability is a characteristic of a system to be able to grow to meet growing amount of work (demand).  In order to meet growing demand MongDB uses sharding to balance the load on a database by taking a large database and breaking it into a number of smaller databases running across multiple servers.  

#### Explain replica sets and sharding

A replica set is an identical data set, copied over to multiple instances.  It provides system redundancy and high availability.  By having multiple copies on multiple servers, possibly in multiple locations, replica sets provide fault-tolerance.  They can also add performance value because clients reading data from servers can use different servers (closer to them) reducing demand to any single server instance.  When changes are made to the Primary, the changes to the oplog are propagated through the system so that the secondaries can perform the same operations.  

Sharding is a method of distributing data across multiple machines.  When load is too much for one server, there are two ways to address the load--Veritical and Horizontal scaling.  Horizontal scaling involved improves the single server through hardware improvements.  Horizontal scaling is done by adding additional servers.   

A sharded cluster each contains a subset of the sharded data.  Each shard can be deployed as a replica set.  The mongos acts as a query router, providing an interface between clients and the cluster.  Config servers store meta data and configuration settings.

Sharding distributes read and write requests, distributes data across shards, and provides high availability.  

#### What is the CAP Theorem?

The CAP theorem states that a distributed data store cannot possible provide more than two out of the three guarantees:
- Consistency - Every read receives the most recent write or an error
- Availability - Every request receives a (non-error) response, without guarantee that it has the most recent write
- Partition Tolerance - The system continues to operate despite messages being dropped or delayed.

#### What does CAP mean for our distributed data stores when they have network problems?

It means that when we have a network problem, we must give up either consistency or availability.  If we give up consistency, it means that the client may receive old data that may not be consistent across our distributed data store.  If we give up availability it means that rather than forward old or inconsistent data, the server is unavailable and doesn't respond until such time that the nodes are synced and the data is consistent across the system.

#### What does it mean that an operation or transaction on a data store is atomic?

#### In Mongo, are operations on embedded documents atomic? 

#### What about operations on referenced documents?



#### What does RDBMS stand for?

Relational DataBase Management System.

#### What about SQL?

Structured Query Language

#### Do SQL databases have embedded records like mongo has embedded documents?

Not usually, in SQL database the standard is towards a normalized form which breaks out related data into separate tables and links them with a foreign key.  

#### Can we freely store any data we like in an RDBMS table the same way we store any data in a mongo collection?

#### What does ACID stand for?
Atomicity
Consistency
Isolation
Durability

#### What does BASE stand for?
Basically Available
Soft state
Eventual consistency

#### What is a SQL dialect?

SQL Dialects are sub-groupings of SQL commands into groups according to their function.

#### What are DML, DDL, DQL?

Data Manipulation Language (Insert)
Data Definition Language (Create)
Data Query Language (Select)

#### What does SELECT do?

Select is used to choose the table that we are working on in a RDBMS.  Once we select, the query will refer to that table when doing its operations
    
####   FROM?

From is use jointly with Select to point to the specific table in our database.
    
####   WHERE?
    
Where is a filtering statement that precedes a predicate that will retrieve records/rows that return true for the predicate.

####  What is a primary key?
    
 A primary key is a unique identifier in our database to identify individual records or rows in our table.
 
####   What is a foreign key?

A foreign key is a column in a table that refers to the primary key of another table in the database.
