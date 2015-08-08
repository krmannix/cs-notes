Joe McCann
	CEO of NodeSource
	@joemccann

	Good APIs get adopted.
	Bad APIs?
	node_modules
	HTTP REST APIs - RestIFY- makes it easy for node
	Async APIs - Don't want API calls to be synchronous and block your main thread
	HTTP SOAP // Yeah right

	Traits of Good APIs
		• Keep it simple
		• Keep it small
		• Keep it consistent
		• Keep it fun
	You have 30 seconds for a developer...
		...to figure out the module's value
		...to understand how to use it
		...to make a good impression

		// ONE WAY

	function fancyMath(seed) {
		this.seed = seed;
	}

	FancyMath.prototype.fancyFunction = function fancyFunction(val) { // do stuff}

	module.exports = FancyMath
	}

	// BESt WAY

	function fancyMath(seed) {
	this.seed = seed;
	}

	// Export just function, abstract difficult part from user
	module.exports = {

	}

	Do one thing and do it well.
	Limit the surface of your API
		• Export a small number of functions
	Abstract the complexities behind a small API

	LevelDB

	API (simple)		Implementation (complex)
	get(key)		|	Snappy Compression. Concepts from Big Table
	put(key, value) |	Stores entries
	del(key)		|	Lexicographically sorted by keys

	Small APIs are Sticier

	Consistent
		 • Only having to learn one set of conventions makes adopting your API that much easier
		 • Underscore.js - works in browser and in server
		 	• Very consistent on Collections
		 	• Understore chain function 

	HTTP Graph API
	https://graph.facebook.com/{user-id}/videos

	Bad Design
	https://api.foo.com/assets/{user-id}?media=phone
	https://api.foo.com/videos?user={user-id}

	How to make APIs fun?
	Enable Instant Gratification!

	Using your API and immediately seeing results are what developers want

	socket.io

	Why-Centric API Design
		• Explain why someone should be using this