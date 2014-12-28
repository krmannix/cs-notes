Ian Maffett
ian.maffett@intel.com

Future of Applications: Intel XDK

• HTML5 Team
	• Software services group inside Intel
	• HTML5 team focuses on runtime, code optimizations and tools.
	• No native SDKs needed to build cross platform mobile applications (Cordova)
	• Lifecycle within XDK
	• What is polymer? - Topeka
	• Simulator based on Rippe
	• Node webkit, backbone.js, node.js, require.js, angular, jQuery (client side), Mocha (server-side test), Promises (Q.js)
	• Desktop app that's really a web app. Chromium up front, node in the back. Single threaded, causes problems with the emulator, so had to change the client/server mentality
	• github.com/rogerwang/node-webkit (Developer at Intel)
	• FRONT-END:
		• Client is using backbone and jQuery. Require loads components. Base developer guidelines are NEEDED. 
		• Component-based: each component is its own entity, but may need to list to other components for events. 
		• Components have their own dependencies too 
	• Server components
		• Normal "backend" server
		• Client code makes calls via HTTP to server components
		• UserFS - wrapper to various file systems
			• Growing plains trying to re-implement an FS
		• Still use some NodeWebkit "magic" for gathering server side objects that developers can use CDT to inspire
	• NodeWebkit MAgic
		• Register components from package.json (it is a Node app)
		• Wrap srver side component calls
	• Adopted Google's JS style guideline
	• Mocha tests for server side
	• Selenium for Client side - user tests and end to end tests for Windows, Mac and Linux
	• JIRA, Crucible for code reviews, Team City for CI/builds, Daily emails about commits/builds,, UI Style guidelines
	• When developer commits, configure git hooks properly to run scripts before push. Check node modules, commit, jshint, etc.
	• CI server will run throughout day and run tests/jshints
	• CI kicks off Daily builds then QA
	• Grunt runs tests locally and creates install gits (minization)

	• Tips:
		• Memory becomes an issue
			• Browser is not reloaded, must manage events properly
			• Using established libraries can help with cleaning up orphaned children
			• Chrome Developer Tools has great tools for tracking down performance issues
		• Focus on UX vs. regular web
			• Don't be slower than a full page reload
			• Make app snappy and fluid
			• Watch flash of contents on repaints
			• Remember browser performance of desktop, mobile and other devices
		• Pick the best tools for the project
			• Don't start a project to learn something
			• Introduce new tools/frameworks on new functionality that can be seperated
			• With the XDK being component based, we are testing React.js in BRackets and Polymer in the core UI framework

	• Web apps are the future:
		• Desktop apps
		• Mobile apps
		• Websites
		• Intranets
		• Portals
		• IoT companion apps - http://xdk-software.intel.com/iot_edition_demo_video
		• In Vehicle Infotainment apps (IVI) - Tizen IVI (HTML5 First)

	• Not Invented Here syndrome
		• This can kill your project. Use existing tools to help scale your development cycle
		• Also for UI/UX - Use existing frameworks & tools
		• Do invent and share your own projects. Thriving community around JS - _join and participate_