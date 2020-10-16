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


#### What are JSON data types?
#### What is BSON?
#### What are some of the data types included in BSON?
#### What is an ObjectId?
#### What is the _id field for in mongo?
#### What does find() do?
#### What is a filter in a mongodb query?
#### What are some examples of filters?
#### What do sort and limit do?
#### What is a projection in a mongodb query?
