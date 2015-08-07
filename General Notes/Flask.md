## Flask - a Python miniframework for web apps

<h5>Intro</h5>
Flask started as an April Fool's joke by Armin Ronacher

<h5>Initialize an App</h5>

'''
from flask import Flask

app = Flask(__name__)
app.run(debug=True, port=8000, host='0.0.0.0')  # debug=True will restart the Flask app when we make changes
'''

This will create a Flask app, and run it in debug mode.
If we now visit `localhost:8000`, nothing will appear. We haven't given Flask an instruction on what to do when that url is reached yet!

<h5>Adding routes</h5>

Adding: 

'''
@app.route('/')
def index():
	return "My favorite color is red"
'''

will specify that when `localhost:8000/` is reached, the webpage will display "*My favorite color is red*""
The decorator `app.route('/')` on the function states that when the `<base url>/` url is reached, this view will be rendered. We could name our function anything, but `index()` fits the current situation. 


<h5>Retrieving request data with query strings</h5>
Often, we will require interaction with our web app. Query strings in GET requests are a common way to pass in arguments that may be used when displaying a view or computing information. To get the query paramaters passed in with a url, we must first import the `requests` library, which comes bundled with Flask. [Click here](http://www.python-requests.org/en/latest/) for more information on the very popular requests library.

At the top of the file below `from flask import Flask`, include the line `from flask import request`

We can now utilize the `requests` library to extract the query paramaters. For this example, we'll pretend we've passed in a `color` argument (__example:__ `<base url>/?color=blue`). To retrieve this portion of the request, we'll need to add to the body of the `index()` function. Example below:

'''
@app.route('/')
def index():
	color = request.args.get('color', 'red')
	return "My favorite color is {}".format(color)
'''

Above, we first use the `get()` function on the `request.args` dictionary, which contains all the query parameters passed in with this specific request. We've also set the default value to `red` if there is no `color` query parameter. We then return the favorite color, formatting the string with whatever value has been passed into the color variable

<h5>Retrieving request data with url arguments</h5>
For cleaner url's, we can embed variables within our routes themselves. The routes will catch the variables, and then pass them into the function with the given variable name. This eliminates a dependence on query strings. Query strings are not necessarily bad, but often result in messy urls and don't support parameter integrity. Paramter integrity might be better seen with an example, but essentually it boils down to the dependence of certain values to be satisfied for an example to be reached. Because a query string is not a foundational part of a url (urls can still be reached with a query string present __or__ absent), expected values cannot be assured to be present.

Let's go back to our color example. We can create an route endpoint that will do the same as our original `index()` function, but without the need for a query string. Example below.

'''
@app.route('/<color>')
def index(color='red'):
	return "My favorite color is {}".format(color)
'''

`color` is defined in the url, and this url cannot be reached unless there is a value in the `color` portion of the url. This may seem silly in this example, but a more complex one is easily imagined. Say your application needs a user identification number and a monentary amount (this may not be the most __secure__ example). To prohibit against non-existant values (although one would still need to ensure correct data types), a route such as `@app.route('/<user_id>/deposit/<monetary_value>/account')` would require both the `<user_id>` and `<monetary_value>` values to be filled.

<h5>Retrieving request data with url arguments, part ii</h5>
If we want to define the types that can be passed into our url arguments, we can define those quite easily.

To only allow for integers in a url argument, change `@app.route('/<color>')` to `@app.route('/<int:color>')`.
This applies to all types, including int, float, and str








