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

