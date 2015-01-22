<h1>SQL</h1>

<h3>From Treehouse DB Foundations course</h3>

* Basic Commands:
	* `SELECT * FROM movies WHERE year = 2003;` _Movies in year 2003_
	* `SELECT * FROM movies WHERE year BETWEEN 1960 AND 2003;` _Movies between 1960 and 2003_
	* `SELECT title, director FROM movies;` _Return certain columns_
* Ordering:
	* `SELECT * FROM movies ORDER BY year;`
		* ADD `ASC` or `DESC` to end of query (after `year`) to change ascending or descending
	* `SELECT * FROM movies ORDER BY year ASC, title DSC;` _Order by year, then within year order reverse alphabetically by title
* Limiting:
	* `SELECT * FROM movies LIMIT 10;` _Limit 10 movies returned_
	* `SELECT * FROM movies LIMIT 10 OFFSET 10;` _Start at the 10th entry_
	* `SELECT * FROM movies LIMIT offset, limitNum;` _Set `offset` and `limitNum` to numbers_
	* `SELECT * FROM movies WHERE year IS NOT NULL;` _Removes any null year rows_
* Creation:
	* `CREATE SCHEMA IF NOT EXIST db_name;` _Creates a database_
	* `USE db_name;` _Selects what database to use_
	* `CREATE SCHEMA DEFAULT CHARACTER SET = utf8;` _Use UTF-8 encoding for DB_
	* __Creating Tables:__
		* `CREATE TABLE actors (name VARCHAR(50));` _Creates actors database with one column, "name"_
		* `CREATE TABLE actors (name VARCHAR(50) NOT NULL);` _Means that column can never contain null values_
		* `CREATE TABLE movies (title VARCHAR(200) NOT NULL, year INTEGER NULL);` _Creates table with 2 columns_
* Interserting, Updating, and Deleting rows
	* Insert
		* `INSERT INTO movies VALUES ("Avatar", 2009);`
		* `INSERT INTO movies (title, year) VALUES ("Avatar", 2009);`
		* `INSERT INTO movies VALUES ("Avatar", 2009), ("Avatar 2", null);`
	* Update
		* `SET SQL_SAFE_UPDATES = 0` _Turn off safe updates_
		* `UPDATE movies SET year = 2015 WHERE title = "Avatar 2";` _Update the row with "Avatar 2"_
		* `UPDATE movies SET year = 2015, title = "Avatar is Back" WHERE title = "Avatar 2";`
	* Deleting
		* `DELETE FROM db_name WHERE prop = value;`
* Alerting Schema
	* `RENAME TABLE table_name_1 TO table_name_2;` _Rename table_
	* `DROP TABLE IF EXISTS table_name;` _Remove table_
	* `TRUNCATE TABLE table_name;` _Deletes table and creates new one with no rows_
	* `ALTER TABLE table_name ADD COLUMN genre VARCHAR(100);` _Add column
	* `ALTER TABLE actor_table ADD (pob VARCHAR(100), dob DATE);` _Add 2 columns_
	* `ALTER TABLE actor_table CHANGE COLUMN pob place_of_birth VARCHAR(100);` _Change column name/type_ __Cannot do multiple columns at once__
	* `ALTER TABLE actor_table DROP date_of_birth;` _Remove column_
	* `DROP DATABASE db_name;` _Removes database_
* Calculating
	* `SELECT COUNT(*) AS review_count FROM movies WHERE year = 1993;` _Counts number of rows that have a year equal to 1993
	* Also have MIN(column), MAX(column), SUM(column), AVG(column)
	* Operations as well - +, /, -
	* `SELECT COUNT(*) FROM movies GROUP BY movie_id;`
	* With joining:
		'SELECT COUNT(*) FROM movies LEFT OUT JOIN reviews ON movies.id = reviews.movie_id GROUP BY movie_id;`
	* If NULL:
		* `SELECT IFNULL(AVG(*), 0) FROM reviews;`
	* `HAVING` keyword lets you filter out rows by their properties
* String functions
	* `LOWER(column)`, `UPPER(column)` _Capitalization_
	* `LENGTH(colulm)`
	* `CONCAT([var num of string args])`
	* `SUBSTRING(string, start_index, end_index)`
	* `TRIM()`
* Server Security
	* Indexing columns for quicker access
		* Indexes are good if you're constantly searching for rows based on a certain column criteria, but will slow down write performance
		* `CREATE INDEX last_name_idx ON users(last_name);`
	* Multiple Users
		* userRead - `GRANT SELECT ON db_name.* TO userRead@'%' IDENTIFIED BY "password";`
		* userReadAndWrite - `GRANT SELECT, INSERT, UPDATE, DELETE ON db_name.* TO userReadAndWrite@'%' IDENTIFIED BY "password";`
		* userAlterSchema - `GRANT ALTER, CREATE, DROP ON db_name.* TO userReadAndWrite@'%' IDENTIFIED BY "password";`
		* After granting privileges, need to run `FLUSH PRIVILEGES;` (If I could spell it right... :p)
	* Backups
		* Path to mysqldump tool for Macs: /usr/local/mysql/bin/mysqldump
		* Can alter SQL query to change database name
* Safe SQLing
	* Normalization is the idea that you can have seperate tables to store data that would go into columns
		* For example, rather than having a string define the gener for a movie, you have an id number - a seperate table exists to store id numbers and their associated genres
	* Keys
		* Primary keys - can't be null, can't be duplicated (Unique identifier)
		* Unique keys - similar to primary keys, except can be null (like a social security number)
		* Foreign keys - Reference data between two tables. Can be duplictated, null 
		* `CREATE TABLES genres (id INTEGER AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50) NOT NULL UNIQUE KEY);`
			* `INSERT INTO genres (name) VALues ("Sci FI");`
		* Add foreign keys as a constraint
			* `ALTER TABLE movies ADD COLUMN genre_id INTEGER NULL, ADD CONSTRAINT FOREIGN KEY (genre_id) REFERENCES genres(id);` _Only allows values to be keys in the genres table in the id column
			* `ALTER TABLE t_movies ADD COLUMN fk_genre_id INTEGER, ADD CONSTRAINT FOREIGN KEY (fk_genre_id) REFERENCES t_genres(pk_id)`
	* Join Tables
		* `SELECT * FROM movies LEFT OUTER JOIN genres ON movies.genre_id = genres.id`
		* `SELECT title, name FROM movies INNER JOIN genres ON genres.id = movies.genre_id`
	* Aliasing 
		* `SELECT name AS title FROM movies;`
	* Grouping
		* `SELECT movies.title, IFNULL(AVG(score), 0) AS average FROM reviews RIGHT OUTER JOIN movies ON movies.id = reviews.movie_id GROUP BY movie_id HAVING average < 2`
