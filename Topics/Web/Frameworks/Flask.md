## Flask - a Python miniframework for web apps

<h3>Part I</h3>

<h5>Intro</h5>
Flask started as an April Fool's joke by Armin Ronacher

<h5>Initialize an App</h5>

Create a file named 'app.py'

```
from flask import Flask

app = Flask(__name__)
app.run(debug=True, port=8000, host='0.0.0.0')  # debug=True will restart the Flask app when we make changes
```

This will create a Flask app, and run it in debug mode.
If we now visit `localhost:8000`, nothing will appear. We haven't given Flask an instruction on what to do when that url is reached yet!

<h5>Adding routes</h5>

Adding: 

```
@app.route('/')
def index():
	return "My favorite color is red"
```

will specify that when `localhost:8000/` is reached, the webpage will display "*My favorite color is red*""
The decorator `app.route('/')` on the function states that when the `<base url>/` url is reached, this view will be rendered. We could name our function anything, but `index()` fits the current situation. 


<h5>Retrieving request data with query strings</h5>
Often, we will require interaction with our web app. Query strings in GET requests are a common way to pass in arguments that may be used when displaying a view or computing information. To get the query paramaters passed in with a url, we must first import the `requests` library, which comes bundled with Flask. [Click here](http://www.python-requests.org/en/latest/) for more information on the very popular requests library.

At the top of the file below `from flask import Flask`, include the line `from flask import request`

We can now utilize the `requests` library to extract the query paramaters. For this example, we'll pretend we've passed in a `color` argument (__example:__ `<base url>/?color=blue`). To retrieve this portion of the request, we'll need to add to the body of the `index()` function. Example below:

```
@app.route('/')
def index():
	color = request.args.get('color', 'red')
	return "My favorite color is {}".format(color)
```

Above, we first use the `get()` function on the `request.args` dictionary, which contains all the query parameters passed in with this specific request. We've also set the default value to `red` if there is no `color` query parameter. We then return the favorite color, formatting the string with whatever value has been passed into the color variable

<h5>Retrieving request data with url arguments</h5>
For cleaner url's, we can embed variables within our routes themselves. The routes will catch the variables, and then pass them into the function with the given variable name. This eliminates a dependence on query strings. Query strings are not necessarily bad, but often result in messy urls and don't support parameter integrity. Paramter integrity might be better seen with an example, but essentually it boils down to the dependence of certain values to be satisfied for an example to be reached. Because a query string is not a foundational part of a url (urls can still be reached with a query string present __or__ absent), expected values cannot be assured to be present.

Let's go back to our color example. We can create an route endpoint that will do the same as our original `index()` function, but without the need for a query string. Example below.

```
@app.route('/<color>')
def index(color='red'):
	return "My favorite color is {}".format(color)
```

`color` is defined in the url, and this url cannot be reached unless there is a value in the `color` portion of the url. This may seem silly in this example, but a more complex one is easily imagined. Say your application needs a user identification number and a monentary amount (this may not be the most __secure__ example). To prohibit against non-existant values (although one would still need to ensure correct data types), a route such as `@app.route('/<user_id>/deposit/<monetary_value>/account')` would require both the `<user_id>` and `<monetary_value>` values to be filled.

<h5>Retrieving request data with url arguments, part ii</h5>
If we want to define the types that can be passed into our url arguments, we can define those quite easily.

To only allow for integers in a url argument, change `@app.route('/<color>')` to `@app.route('/<int:color>')`.
This applies to all types, including int, float, and str

<h3>Part 2</h3>

<h5>Returning HTML</h5>
So far, we've returned plain text. This will obviously not work as we expand our site and want our views to contain anything beyond simple text.

In Flask, there is a special place we can put our HTML files. At the root level, add a `templates` folder, where we'll place HTML files. Within templates, create a file named `index.html`. For now, we'll add something super basic, like below:

```
<!doctype html>
<html>
	<head>
		<title>Simple Flask</title>
	</head>
	<body>
		<h1>Our first Flask view</h1>
	</body>
</html>
```

In conjunction with the special `templates` folder, we'll want to utilize a function Flask provides called `render_template(<view>, **kwargs)`. We'll pass in the view we want to display, along with any arguments we might need in our HTML file. Right now, we don't utilize any arguments, but as Flask inherently uses jinja2 as it's rendering engine, we'll be able to dynamically load web pages & HTML. For the simple `index.html`, we'll just need to call `render_template("index.html")`. Example below (within `app.py`):

```
from flask import render_template  # add this at the top to import the render_template() function


@app.route('/')
def index():
	return render_template("index.html")
```

<h5>Dynamic HTML</h5>

We acknowledge the ability to pass in variables and have them load into our HTML page. We'll do the following to illustrate this:

Replace the `<h1>` tags of our HTML with `<h1>My name is {{ name }}</h1>`. Flask will look for a variable passed into named `name`, and replace `{{ name }}` with that variable. This won't currently work until we explicitly pass that variable into the `render_template()` function, show below:

 ```
@app.route('/')
def index():
	return render_template("index.html", name="Kevin")  # Replace "Kevin" with whatever your name is
```

`render_template()` can take any number of values after defining the HTML template we wish to use, and those variables will then be available within the HTML to replace our placeholders, defined by `{{}}`.

<h5>DRY HTML</h5>
We often have HTML that will need to be included in many views. We recycle this HTML through template inheritance, which allows developers to cutdown on reused code, and change the layout of many HTML pages by only updating one HTML file. 

For example, we may have a base HTML file that will include navigation bars or recurring headers. 

In Jinja, when we use the `{% %}` markers (as opposed to what we previously used `{{ }}`), we are stating that we want an action to occur. In our base HTML file, which we'll call `base.html`, we'll do as below:

```
<!doctype html>
<html>
	<head>
		<title>{% block title %}{% endblock %}</title>
	</head>
	<body>
		<h1>{% block content %}{% endblock %}</h1>
	</body>
</html>
```

We've created two blocks, `title` and `content`. We'll now "import" these `base.html` file (which should be located in the templates folder, as before) and then replace these blocks in our individual HTML files.

In our `index.html` file, let's now create the content that we want to replace the `title` and `content` blocks with.


```
{% extends "base.html" %} <!-- Imports the base.html file -->

{% block title %}Simple Flask, Part II{% endblock %} <!-- Replaces the section of title block -->

{% block content %}Flask is really cool!!{% endblock %} <!-- Replaces the section of content block -->
```

We can also add in more complex content, using regular HTML tags and the like. Essentially, everything defined in `{% block <name> %}{% endblock %}` will replace the block with the same name in the extended HTML file.

<h5>Static files (CSS, JS, etc)</h5>
Just like the `template` folder, we can add a `static` folder which is a special folder as well. We'll house our stylesheets and JavaScript files within this folder. For the sake of brevity, we won't actually add anything in our CSS file, but we'll create one. From the root directory, create the `static` folder, and a `styles.css` file within that folder.

In our base.html, we'll use add a line in the `<head>` section:

`<link rel='stylesheet' href='/static/styles.css'>` 

`/static` will always refer to our static directory through development, allowing our content files (HTML) and our style/behavior files (CSS & JS) in seperate folders. Combined with blocks, we can also indentify specific stylesheets with specific pages

<h3>Part III</h3>

<h5>Forms in Flask</h5>
If you are familiar with HTML forms, we can integrate forms with Flask. 

Let's create a route & function named `submit`, like below:

 ```
@app.route('/submit')
def submit():
	return "Submitted!"
```

A route now exists that is paired with the function `submit()`. In our HTML file (we can create a new one), we will now direct the `action` attribute of the `<form>` element to find the route of the `submit()` function. Example below:

```
<!doctype html>
<html>
	<head>
		<title>Flask Forms</title>
	</head>
	<body>
		<form method="post" action="{{ url_for('submit') }}">
			<h1>Your Name!</h1>
			<label for="name">Name</label>
			<input type="text" id="name" name="your_name">
			<button type="submit" id="submit_button">Submit</button>
		</form>
	</body>
</html>
```

We tell the form to use the HTTP POST method, and use Flask's built in `{{ url_for() }}` function to get the correct url for the `submit()` function.










