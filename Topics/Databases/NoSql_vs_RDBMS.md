Rudimentary database design and proper usage is the basic responsibility of developers, and if you don't know it then it is your responsibility to learn it.

<h4>Definitions</h4>

_NoSQL:_ Not Only SQL

_Distributed System:_ Where components exist on networked computer coordinate through passed messages. Characteristics include concurrency of components, lack of a global clock, and independent device failure. In terms of databases, not all storage devices are attached to a common CPU and consist of loosely-coupled sites that share no physical components. Can sometimes speed up transactions due to many machines being able to process transactions, but may also introduce long latencies and unexpected failures.

_Replication:_ Looks for changes in and then spreads these changes out to all the databases in the cluster/system. Can be complex, time & resource consuming.

_Duplication:_ There is one __master__ database, and at certain hours this is duplicated to all other databases

_ACID:_
	* Atomicity - each transaction is __all or nothing__
	* Consistency - each transaction brings the database from a valid state to a valid state
	* Isolation - Concurrent transcations need to equal in-theory serial transactions
	* Durability - Once a transaction is committed, it will remain so even in the event of a crash or power loss

_CAP Theorem:_
	For properties of a distributed system out of the following 3, you can only have 2:
		* Consistency
		* Availability
		* tolerance to network Partioning

_Neo4j_: Graph NoSQL database

_CouchDB:_ document databases

_db40:_ Object databases

_MongoDB:_
	* Supports `mongodb` locking - i.e., all connections to the database will be locked on a write, including reads. However, locks different than SQL and will be held for about a microsecond between average updates



## MySQL ##

* Doesn't grow well in a distributed system 
* Scales well vertically, but doesn't scale well when adding more servers to share the load i.e. horizontally
* Simple way of representing data / business models
* SQL is easy-to-use 
* Bulletproof data integrity & security without having to rely on application logic

<h3> Table Types </h3>

<h4>InnoDB:<h4>

<h5>Advantages</h5>
	* Data integrity and foreign key constraints
	* Recover well from crashes
	* Supports transactions (multiple SQL commands to be treated as a single unit)
	* _Row-level locking, so the entire table is not locked_
	* InnoDB designed for maximum performance when processing high volume of data

<h5>Disadvantages</h5>
	* Can't scale well in a distributed system
	* Has an upper limit (essentially) of storage before complexity sets in
	


MyISAM:

<h5>Advantages</h5>
	* Very easy - it's simple, where one only needs to determine column data type
	* Speedy (MySQL as a whole is quick)
	* MyISAM designed for need of speed
	* Full-text searching & order by relevance

<h5>Disadvantages</h5>
	* Does not support transactions or foreign keys - poor data integrity
	* Can become corrupt after a table crash
	* Table-level locking. Is bad for tables with alot of inserts 

<h5>Why use it?</h5>
	* New to MySQL
	* Webapp is simple & needs to be fast

## NoSQL ##

Has become popular because when a relational database grows out of one server, it's no longer very easy to use - they don't scale well in a distributed system. For really big sites (think Google, Yahoo, Facebook & Amazon) they store their data in distributed systems for several reasons. Thus, NoSQL is an alternative.

You can get impressive performance if you're okay with taking a risk of potentially losing data, because NoSQL sometimes gives up ACID attributes to boost speed. For example, MongoDB stages data changes to be written when it's convenient. While it's safe and transactionally secure, it's kept in volatile storage meaning that if one loses power one can't be sure that there hasn't been lost data or corrupted table. 



The logical design of the database should be centered around data analysis and user requirements; the choice to use a relational database would come later, and even later would the the choice of MySQL as a relational database management system, and then the selection of a storage engine for each table.