Steve Marx (617) 616 8616
@smarx
PLAYING WITH APIS

This Talk:
	Fun
	A bit silly
	A bit informative
	Occasionally practical


First demo:
	SMS to QR
	Twilio - takes a text message and can send it to a forwarded "platform"
	Objective: Receive text messages on phone

	local url  = 'https://api.qrserver.com/v1/create-qr-code/?'
	Sends text to API that converts strings to QR codes
	pusher API
	 - way to send through web socket from server to client

Chuck Nerdis:

	Objective: LEarn about Chunk Norris technical prowess while listening to soft jazz

	Purely Javascript/HTML in the browser app

	$.get(
		'http://api.icndb.com/jokes/random?limitTo=[nerdy]',
		function (data) {
			nextJoke = htmlDecode(data.value.joke); // Had to write decode function
		});
	);

	Text to speech: http://tts-api.com/tts.mp3?q=' + encodeURIComponent("hi"))[0].play();
	Cool background: GeoPattern.generate(nextJoke).toDataUrl()


Github Center

	Objective: Receive dopamine when I "git push"

	var client = new WebSocketClient();

	client.connect()

	WebHooks: Instead of you calling API, API calls you. API can send a request to "me", using pusher

Arithmetic of Crowds

	Objective: achieve high mathematical precision
	api.polleverywhere.com/free_text_polls // Need headers to be {'Accept:' 'application/json'}


Quarterly Chees Review

	postmarkapp.com
	mailgun.com
	sendgrid.com
	kenn.io

Schrodinger's Files:

	Objective: Something bout quantum mechanics

	Deletes files randomly with a 50% chance

	• Dropbox has WebHooks
	• 

RemYote Control

	Objective: Have a remote control for my slides
	Uses YO 

	twilio.com
	pusher.com
	goqr.me
	icndb.com
	tts-api.com
	github.com/btmills/geopattern
	postmarkapp.com
	dropbox.com/developers
	developer.github.com
	api.polleverywhere.com
	yoapi.justyo.co

	smarx@smarx.com
	@smarx
	smarx@dropbox.com

	runscope
	Traffic & Weather.io