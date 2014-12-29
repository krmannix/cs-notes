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
