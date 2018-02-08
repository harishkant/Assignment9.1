# Assignment9.1

Question 1: What is NoSQL data base?

Answer:	A NoSQL (originally referring to "non SQL" or "non relational") database provides a mechanism for storage and retrieval of data that is modeled in means other than the tabular relations used in relational databases. ... NoSQL databases are increasingly used in big data and real-time web applications


Question 2:	How does data get stored in NoSQl database?

Answer:	Relational databases store the vast majority of web application persistent data. However, there are several alternative classifications of storage representations.
Key-value pair
Document-oriented
Column-family table
Graph
These persistent data storage representations are commonly used to augment, rather than completely replace, relational databases. The underlying persistence type used by the NoSQL database often gives it different performance characteristics than a relational database, with better results on some types of read/writes and worse performance on others.
Key-value Pair
Key-value pair data stores are based on hash map data structures.
Key-value pair data stores
Redis is an open source in-memory key-value pair data store. Redis is often called "the Swiss Army Knife of web application development." It can be used for caching, queuing, and storing session data for faster access than a traditional relational database, among many other use cases. Learn more on the Redis page.
Memcached is another widely used in-memory key-value pair storage system.
Key-value pair resources
What is a key-value store database? is a Stack Overflow Q&A that straight on answers this subject.
Redis resources
How to Use Redis with Python 3 and redis-py on Ubuntu 16.04 contains detailed steps to install and start using Redis in Python.
"How To Install and Use Redis" is a guide for getting up with the extremely useful in-memory data store.
This video on Scaling Redis at Twitter is a detailed look behind the scenes with a massive Redis deployment.
Walrus is a higher-level Python wrapper for Redis with some caching, querying and data structure components build into the library.
Real World Redis Tips provides some guidance from Heroku's engineers from deploying Redis at scale. The tips include setting an explicit idle connection timeout, using a connection pooler and avoiding using KEYS in favor of SCAN.
Writing Redis in Python with Asyncio shows a detailed example for how to use the new Asyncio standard library in Python 3.4+ for working with Redis.
How to collect Redis metrics shows how to use the Redis CLI client to grab key metrics on latency.
You should revise your Redis max connections setting is a retrospective from a hard web application failure due to Redis connections maxing out on Heroku, and how to avoid this in your own applications by modifying your redis.conf settings.
Document-oriented
A document-oriented database provides a semi-structured representation for nested data.
Document-oriented data stores
MongoDB is an open source document-oriented data store with a Binary Object Notation (BSON) storage format that is JSON-style and familiar to web developers. PyMongo is a commonly used client for interfacing with one or more MongoDB instances through Python code. MongoEngine is a Python ORM specifically written for MongoDB that is built on top of PyMongo.
Riak is an open source distributed data store focused on availability, fault tolerance and large scale deployments.
Apache CouchDB is also an open source project where the focus is on embracing RESTful-style HTTP access for working with stored JSON data.
Document-oriented data store resources
The creator and maintainers of PyMongo review four decisions they regret from building the widely-used Python MongoDB driver.
start_request
use_greenlets
copy_database
MongoReplicaSetClient
The Python and MongoDB Talk Python to Me podcast has a great interview with the maintainer of the Python driver for MongoDB.
MongoDB queries don’t always return all matching documents! is a walkthrough of discovering how MongoDB queries actually work, and shows some potential pitfalls of relying on technologies where you do not fully understand how they operate.
Introduction to MongoDB and Python shows how to use Python to interface with MongoDB via PyMongo and MongoEngine.
Column-family table
A column-family table class of NoSQL data stores builds on the key-value pair type. Each key-value pair is considered a row in the store while the column family is similar to a table in the relational database model.
Column-family table data stores
Apache Cassandra
Apache HBase
Graph
A graph database represents and stores data in three aspects: nodes, edges and properties.
A node is an entity, such as a person or business.
An edge is the relationship between two entities. For example, an edge could represent that a node for a person entity is an employee of a business entity.
A property represents information about nodes. For example, an entity representing a person could have a property of "female" or "male".
Graph data stores
Neo4j is one of the most widely used graph databases and runs on the Java Virtual Machine stack.
Cayley is an open source graph data store written by Google primarily written in Go.
Titan is a distributed graph database built for multi-node clusters.
Graph data store resources
Introduction to Graph Databases covers trends in NoSQL data stores and compares graph databases to other data store types.



Question 3: What is a column family in HBase?

Answer: In the HBase data model columns are grouped into column families, which must be defined up front during table creation. Column families are stored together on disk, which is why HBase is referred to as a column-oriented data store
Logical View of Customer Contact Information in HBase
Row Key                   Column Family: {Column Qualifier:Version:Value}
00001                     CustomerName: {‘FN’:
                          1383859182496:‘John’,
                          ‘LN’: 1383859182858:‘Smith’,
                          ‘MN’: 1383859183001:’Timothy’,
                          ‘MN’: 1383859182915:’T’}
                          ContactInfo: {‘EA’:
                          1383859183030:‘John.Smith@xyz.com’,
                          ’SA’: 1383859183073:’1 Hadoop Lane, NY
                          11111’}
00002                     CustomerName: {‘FN’:
                          1383859183103:‘Jane’,
                          ‘LN’: 1383859183163:‘Doe’,
                          ContactInfo: {
                          ’SA’: 1383859185577:’7 HBase Ave, CA
                          22222’}


The table shows two column families: CustomerName and ContactInfo. When creating a table in HBase, the developer or administrator is required to define one or more column families using printable characters.
Generally, column families remain fixed throughout the lifetime of an HBase table but new column families can be added by using administrative commands. The official recommendation for the number of column families per table is three or less. 


Question 4: How many maximum number of columns can be added to HBase table?
Answer: Many HBase users start to design HBase tables before reading about it and before knowing about all the HBase features and behaviors. People coming from the RDBMS world, with no knowledge of the differences between a column family and a column qualifier, will be tempted to create a column family for each column they have of a table they want to migrate to HBase. As a result, it is common to see tables designed with too many column families.
For years, it has been recommended to keep the number of column families under three. But there is no magic number like this. Why not two? Why not four? Technically, HBase can manage more than three of four column families. However, you need to understand how column families work to make the best use of them. The consequences explained here will give you a very good idea of what kind of pressure column families are putting on HBase. Keep in mind that column families are built to regroup data with a similar format or a similar access pattern. Let’s look at these two factors and how they affect the number of column families

Question 5: Why columns are not defined at the time of table creation in HBase?
Answer: Columns in Apache HBase are grouped into column families. All column members of a column family have the same prefix. For example, the columns courses:history and courses:math are both members of the courses column family. The colon character (:) delimits the column family from the . The column family prefix must be composed of printable characters. The qualifying tail, the column family qualifier, can be made of any arbitrary bytes. Column families must be declared up front at schema definition time whereas columns do not need to be defined at schema time but can be conjured on the fly while the table is up an running.
Physically, all column family members are stored together on the filesystem. Because tunings and storage specifications are done at the column family level, it is advised that all column family members have the same general access pattern and size characteristics.

Question 6: How does data get managed in HBase?
Answer: HBase is a distributed column-oriented database built on top of the Hadoop file system. It is an open-source project and is horizontally scalable.
HBase is a data model that is similar to Google’s big table designed to provide quick random access to huge amounts of structured data. It leverages the fault tolerance provided by the Hadoop File System (HDFS).
It is a part of the Hadoop ecosystem that provides random real-time read/write access to data in the Hadoop File System.
One can store the data in HDFS either directly or through HBase. Data consumer reads/accesses the data in HDFS randomly using HBase. HBase sits on top of the Hadoop File System and provides read and write access.

Storage Mechanism in HBase
HBase is a column-oriented database and the tables in it are sorted by row. The table schema defines only column families, which are the key value pairs. A table have multiple column families and each column family can have any number of columns. Subsequent column values are stored contiguously on the disk. Each cell value of the table has a timestamp. In short, in an HBase:
Table is a collection of rows.
Row is a collection of column families.
Column family is a collection of columns.
Column is a collection of key value pairs.


Question 7: What happens internally when new data gets inserted into HBase table?
Answer: When a put/insert request is initiated, the value is first written into the WAL and then into the memstore. The values in the memstore is stored in the same sorted manner as in the HFile. Once the memstore is full, it is then flushed into a new HFile. 










