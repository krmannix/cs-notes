<h1>Ember</h1>


<h3>Intro</h3>
* For creating ambitious web pages. 
	* This is do dynamically change and consider the state of a webpage, without having to reload whole HTML/CSS/JS files
* Convention over Configuration
* Two-way data binding
* ORMs abstracts away a lot of backend
* Views built in HTML
* If using Node.js, using Express.js as well

<h3>Basics</h3>
* __Ember uses Handlebar templates and jQuery__
	* Handlebar templates define where data will go within a dynamic HTML page
		* Called with script tags like so: `<script type="x-type/handlebars"></script>`
* __How it works__
	1. HTML with no literal content is loaded, just structure
	2. JS Framework comes and instantiates application, router, route, then models explicity, and controllers/view implicitly
	3. Loads templates embedded within HTML
	4. Processes those templates, interpolating model data and rendering it to a page
	* Need to start a simple web server to ensure our data doesn't get cached by the browser during development
		* For Python: `python -m SimpleHTTPServer` within directory of project
	*  In JS, start with line `App = Ember.Application.create();`
* __Data Binding__
	* App.name = "Your Name" creates global variable "name", can be binded in HTML
		* For example: `<h2>This is {{name}}'s webpage.</h2>`
	* Can also set way to get data
		* `<h2>{{view Ember.TextField valueBinding="App.name"}}</h2>`
		* Then, running `App.get('name')` will return whatever data is in the text field
* __Where's All The Code??__
	* Ember does not create "new files" like Ruby on Rails
		* Creation of instances happen in memory
			* This makes it harder to debug in a way
			* When new version is released, don't need to recompile all files. Just update version #
	* _Open initialization, searches directory for `ApplicationRoute` or `ApplicationController` and a template with `data-template-name="application"` or the first template in a page without `data-template-name="application"`_
* __What's a router?__
	* Javascript implementation to "capture" urls, and then act on it
		* Instead of fetching static files, use url to dynamically generate different content with same template
		* Craze of "Single Page Apps"
	* "Stuff that translates urls to application states and back"
* __Ember's Lifecycle__
	1. HTML Page loads
	2. _app.js_ instantiates Ember Application
	3. Looks for `ApplicationRoute` & `ApplicationController`, if you didn't define one, it loads it's own
	4. Looks for application template in HTML and hooks it up with `ApplicationController` if there is one
	5. If at index of page, looks for `IndexRoute` in _app.js_ as well as `IndexController`
	6. Will find template named _index_ in the HTML document and render it to the _outlet_ helper in the application template
* __Controllers__ - how app behaves. __Templates__ - how app looks

<h3>Ember Boilerplate and Workflow</h3>
* __Possible Boilerplate/Tools__
	* Yeoman _(This is the one we'll use)_
		* Yo (Boilerplate set-up)
		* Grunt (Task runner)
		* Bower (manage application dependencies)
	* Ember Tools
		* Will be merged into the core of Ember in the future and uses Browserify (converts npm modules into web-usable)
	* Ember App Kit
		* Alternative to Yeoman
		* Will become core of offical Ember Tools
	* Ember Rails
		* Gem for Ruby to work with the Rails Asset Pipeline
	* Ember CLI
		* Unstable for now - could be cool in the future
* __Installing Yeoman & Dependencies__
	* `npm install -g yo grunt-cli bower`
		* Might need to uninstall previously-installed Grunt with `npm uninstall -g grunt`
	* Ruby (default on Mac)
	* Compass
		* `gem install compass`
	* Install generator
		1. `yo`
		2. `Install a generator`
		3. Search: `ember`
		4. Install `generator-ember` (or use `npm install -g generator-ember`)
	* Now, everything should be installed...
* __Running the Generator__
	* `yo` -> `Run the Ember generator` (might need to install 'chalk' npm package)
	* Makes 3 files
		* _app_
			* Contains all application files
		* _node_modules_
			* All application dependencies
		* _test_
			* Configuration and test files
	* _Grunt_ is a Task Runner that's bundled with Yeoman
		* To build the application, run `grunt`
		* To view the app, run `grunt serve`
		* We can also run tests (in Mocha??)
			* Run `grunt test`
	* Use the Ember Insepctor for Chrome or Firefox to debug the application

<h3>Building the Prototype: Templates</h3>
* We're going to start with our HTML Templates. We use Handlebars
* Start first with HTML templating, no Handlebars yet
* Before, we used `<script>` tags to to embed templates. This is expensive.
	* We can precompile by putting them all in a _handlebars.runtime.js_ file
	* __Yo__ will generate handlebars templates for us with an _.hbs_ extension, while __Grunt__ will watch, compile & concatenate them
		* We'll need to tell Grunt where to look with:

	grunt.initConfig({
		yeoman: yeomanConfig,
		watch: {
			emberTemplates: {
				files: '<%= yeoman.app %>/templates/**/*.hbs',
				tasks: ['emberTemplates', 'connect:livereload']
			}
		}
	});

	* Move to _.hbs_ files for real work, but it's fine to use `<script>` tags for sketches or small jobs
* __VARIABLES__
	* One example of using variables is such:
		* In _app/scripts/app.js_ add the line `appvarattopofscreen.applicationName = "Name"`
		* Now, in Handlebar templates where you want to use the name, add `{{appvarattopofscreen.applicationName}}`
	* __#link-to__: Let's add a link on this to the main page
		* Change the previous line to `{{#link-to "index" class="navbar-brand"}}{{appvarattopofscreen.applicationName}}{{/link-to}}
		* While we haven't added controllers or routers, Ember adds default ones. For example, the _IndexRoute_
	* __Handlebars__ is similar to HTML
		* `{{` -> `<` and `}}` -> `>`
		* `#link-to` is the opening tag
		* We can declare attributes in Handlebars tags
		* For the string "Index", __Handlebars__ has a naming convention
			* For #link-to, you pass a route by name
			* Take the camelcase of the route, remove _Route_, insert a hyphen before every capital (except the first), and make all letters lowercase
				* For example `IndexRoute` -> `route` or `SearchResultsRoute` -> `search-results`
	* __input__:
		* Example: `{{input type="text" class="search-input" placeholder="Search for artists or songs"}}` 
	* What is __{{outlet}}__??
		* We don't quite know yet (we'll learn next chapter)
		* For now, we are rendering the content associated with `IndexRoute` and _index.hbs_ into the {{outlet}} of _application.hbs_
	* __each__:
		* We can iterate through `<ul>` like this, makes it very easy. For example:

	<ul class="search-results artists">
		{{#each Rockandroll.dummySearchResultsArtists}}
		<li><a href="#">{{name}}</a></li>
		{{/each}}
	</ul>

		* This is if our variable `Rockandroll.dummySearchResultsArtists` has a field in the array of objects of `name`
		* We could also do: `{{#each artist in Rockandroll.dummySearchResultsArtists}}<li><a href="#">{{artist.name}}</a></li>{{/each}}
	*__if & else__:
		* We can use `{{#if nickname}} <...> {{else}} <..>`
		* {{#if nickname}} evaluates to false if: _false, null, undefined_ and `[]`
	*__action__:
		* Capture action with (for example) `<button {{action 'viewArtist' this}}>CLICK</button>
			* Then, we need to handle this action by our controller. If we don't have a controller yet, create a new file and controller like:
				* `__app/scripts/controllers/index_controller.js`
				* `Rockandroll.IndexController = Ember.Controller.extend({});`
					* Doing this, we are overriding the default controller ember created
				* When using actions, for example, you can add an object to the `.extend({})`:
					
	actions: {
		viewedArtist: function(artist) {
			console.log("Got " + artist.name)
		}
	}

	*__bind-attr__:
		* This is to dynamically alter the attributes of any any HTML tag
			* For example `<a {{bind-attr href="model.license.url"}}>`
			* Another example `<img {{bind-attr src="model.image.url"}} class="image-class">`
* __CREATING CUSTOM HELPERS__
	* We can register `helpers` through Handlebars to build custom tags
	* In this case, this was put in the app.js file, as such:

	Ember.Handlebars.helper('hotttnesss-badge', function(value, options) {
		...
		return new Handlebars.SafeString(html);
	});

	* Then, we can call hotttness-badge as a handlebar element: `{{hotttnesss-badge model.hotttnesss}}
		* We pass in a `value` to `value`, which can then be acted on

<h3>Building the Prototype: The Router, Routes & Models</h3>
* The URL is key in giving people a way to start where they left off. It includes state data, etc.
* __Router__
	* A logical mechanism that routes things
	* A request comes in and the route delivers the right models, views, controllers & templates
	* Two things needed:
		* Map - this maps out each possible url and grabs the right data, and generates the app
		* Route - the map will be search for a route
	* Up to this point, we haven't needed a map. This is because Ember fills in a lot of these details automatically through convention
	* To add a router, update the function in the _app/scripts/router.js_ to complete the map
		* We didn't add an index or application route because those are automatically generated

		Rockandroll.Router.map(function () {
		  this.route('search-results');
		  this.route('artist');
		  this.route('song');
		});

	* Wildcards are also possible, and "masking" of routes:
		* `this.route('search-results', { path: 'search/:term' });`
* __Models__
	* Unlike controllers & views, models are necessarily nestled with one particular view
	* The model allows for de-serialization of the URL into model/state data
	* Create a model with `Rockandroll.Artist = Em.Object.extend({ id: null, name: null });`
	* Initialize a model with `var artist = Rockandroll.Artist.create({ id: '123xyz', name: 'Spongebob'});`

* __Putting it together__
	* Now that we know abour Routers & Models, we can create the Artist Route. In _app/scripts/routes/artist_route.js_:

	Rockandroll.ArtistRoute = Ember.Route.extend({
		model: function(params) {

		}
	});

	* For this application, we'll need to use Promises
	* __Promises__
		* Promises have not been officially implemented/supported, but will be soon. So, Ember has a few different Promise "flavors"
		* jQuery: `Ember.$.getJSON(url, obj).then(function(data) { /* Insert code here */});`

<h3>Building the Prototype: Controllers, Views, Data Binding, and Events</h3>
* Controllers are for transient state data
* Controllers have these 4 important jobs (among others):
	1. Manipulate the data within the application's models
	2. Store transient data, whether standalone or data received from models
	3. Listen to events dispatched, and dispatch events
	4. Instigate the transition from one state to another
* Currently, we can't really _do_ anything. We can't search in our application. Let's change that
	* In _app.js_, add a controller like:
		* `Rockandroll.ApplicationController = Ember.ObjectController.extend({});`
		* Withing the extended Object controller, we can add _variables_ and _actions_

	Rockandroll.ApplicationController = Ember.ObjectController.extend({
		searchTerms: '',
		applicationName: "Rock 'n' Roll",
		actions: {
			submit: function() {
				this.transitionToRoute('search-results', this.get('searchTerms'));
			}
		}
	});


	* The `actions` object holds all event handlers fired by the templates
	* To bind the data in our input textbox to the `searchTerms` variable, add `valueBinding="controller.searchTerms"` to the `<input>` tag
	* There is now a `submit` helper, but an instance to fire this event needs to be added. 
		* In the _application.hbs_, add `{{action "submit"}}` within the button tag and `action="submit"` in the `<input>` tag
			* It's obvious why the button get's the action, but the input box gets it so if a user hits enter, the event will fire
* __Computed Properties__
	* This is one of Ember's biggest draws. 
	* Allows variables to "watch" and be changed when other things in the app change
	* For example, in the ApplicationController:

	applicationName: function() {
		var st = this.get('searchTerms');
		if (st) {
			return st + "???";
		} else {
			return "Rock N Roll";
		}
	}.property('searchTerms')

* Use `get()` and `set()` whenever possible
	* It makes sure you get the latest value of a variable, and set notifies variables watching the set variable of changes
* Routes can pass data into the static Handlebars templates
* __Views__
	* Views allow for more custom widgets within a template
	* A more complex "computed property"
	* `didInsertElement` is like `$().ready()` for a jQuery element, called once the view is injected into the page
	* Can also add a click button, like so: 

	Rockandroll.SongView = Em.View.extend({
		click: function(jQueryEvent) {
			console.log(jQueryEvent.target);
		}
	});

<h3>Persisting Data</h3>
* __Ember Data__
	1. Loads data from a persistence layer
	2. Maps the data to a set of client-side models 
	3. Updates the Models
	4. Saves and syncs the data with the persistence layer
* Setting up the Router & Activity View for the Activity State
* __Every route has an associated model__
	* The _model_ method is used to set up the plumbing between a particular model and a route
* `{{#link-to 'activity'}}` instead of an `<a href>` tag routes to the activity, and will look for a model
* For working with the persistence in Ember Data, use `DS` rather than `Ember` - i.e., `DS.Model.extend({});`
	* For object members, use `DS.attr('string');` or `DS.attr('number');`
* Fixtures are a way to put sample data into an application before connecting the application to long-term persistence
* To go over actions again: `<a {{action 'viewedArtist' this }}>{{name}}</a>`













	

