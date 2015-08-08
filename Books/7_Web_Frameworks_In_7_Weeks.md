<h1>Web Frameworks</h1>

<h2>Sinatra</h2>
	* Hello World in Sinatra
		_sinatra/hello/app.rb_
		require "sinatra"
		get "/hello" do
		"Hello, Sinatra"
		end
	* In a GET request to /hello, "Hello, Sinatra" will be the response
	* If a method call and route match, then the code block below is ran
	* Particularly useful to build a RESTful API Server
<h4>Day 1: Building a Bookmark Application</h4>
	* `gem install sinatra`
	* Create file named _app.rb_ 
		* Put above code block in it
	* Then, run with: `ruby app.rb`
	* __Installing RSpec, a testing suite__
		* `gem install rspec rack-test`
		