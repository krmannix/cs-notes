* Deploy to Heroku
	* `git push heroku master`
* A Procfile declare process types and start scripts
* To start one heroku dyno
	* `heroku ps:scale web=1`
* Run app locally
	* `foreman start web`
* See app on Heroku
	* `heroku open`

<h6>Config variables</h6>
* Set config variables
	* `heroku config:set TIMES=2`
* View config variables
	* `heroku config`

<h6>Add-ons</h6>
* Visit this [url](https://addons.heroku.com/) to see all that can be added
* Add database to app
	* Adds in an environmental variable named `DATABASE_URL`
	* `heroku addons:add heroku-postgresql:hobby-dev` _I'm assuming hobby-dev means the price level_
* Open up connection to database from terminal
	* `heroku pg:psql`
	* Then, enter some SQL
* Example Postgres function

	var pg = require('pg');

	app.get('/db', function (request, response) {
	  pg.connect(process.env.DATABASE_URL, function(err, client, done) {
	    client.query('SELECT * FROM test_table', function(err, result) {
	      done();
	      if (err)
	       { console.error(err); response.send("Error " + err); }
	      else
	       { response.send(result.rows); }
	    });
	  });
	})