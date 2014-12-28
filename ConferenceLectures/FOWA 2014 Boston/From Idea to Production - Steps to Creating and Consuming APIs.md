Mike Adler (Constant Contact)

APIs are OLD!!
	• APIs use to be url-based, url/paramter, and then just getting XML
	• IMlogic wrote an Instant Messaging API
	• Symantec
	• Constant Contact - "Best APIs out there"
		• More than a billion API calls in 2014
		• 6,000 developers
	Start at the beginning
		SOAP
		REST

	1. READ/WRITE the Documentation First
		• If you're creating one, do the same. Make sure the use case makes sense
		• What nouns will you be using. 
	2. Figure out the stuff that KILLS you later
	3. Remember we write code - don't worry about not being "RESTful"
	4. Versioning. How are we going to Version our APIs?
		1. Whack the API version into the URL
		2. Custom request header - use same URL but uadd header such as "version-2"
		3. Change Accept header
	5. Authentication/Authorization
		1. Don't use username password or no Authentication
		2. Use keys to know who is using our APIs
	6. State
		1. Don't keep state between calls

Keep calm and write code
Test
	• Are all results covered?
	• How long does it take the call to return?
Instrumenting
	• What does this mean??

Build Sample Programs
	• REALLY, REALLY important
Constant Contacts creates "Data Factories"
Automate Testing Environments, not Just Tests

Make it Public
	• AND MAKE A PORTAL!
		• Documentation
		• Sample Programs
		• Dashboards - How is my API performing
		• Support (Community)

The Rest
	• Communicate
	• Keep It Simple (Stupid)
	• Focus on Building & Using Value