Rudimentary database design and proper usage is the basic responsibility of developers, and if you don't know it then it is your responsibility to learn it.

<h4>Definitions</h4>
_Distributed System_: Where components exist on networked computer coordinate through passed messages. Characteristics include concurrency of components, lack of a global clock, and independent device failure. In terms of databases, not all storage devices are attached to a common CPU and consist of loosely-coupled sites that share no physical components. Can sometimes speed up transactions due to many machines being able to process transactions, but may also introduce long latencies and unexpected failures.

_Replication_: Looks for changes in and then spreads these changes out to all the databases in the cluster/system. Can be complex, time & resource consuming.

_Duplication_: There is one __master__ database, and at certain hours this is duplicated to all other databases

## MySQL ##

* Doesn't grow well in a distributed system 

<h3> Table Types </h3>

<h4>InnoDB:<h4>

<h5>Advantages</h5>
	* Data integrity and foreign key constraints
	* Recover well from crashes
	* Supports transactions (multiple SQL commands to be treated as a single unit)
	* _Row-level locking, so the entire table is not locked_
	* InnoDB designed for maximum performance when processing high volume of data


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




The logical design of the database should be centered around data analysis and user requirements; the choice to use a relational database would come later, and even later would the the choice of MySQL as a relational database management system, and then the selection of a storage engine for each table.