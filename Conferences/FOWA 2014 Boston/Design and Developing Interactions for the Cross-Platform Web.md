Matt Keas
http://mkeas.org
The Iron Yard

1. DOM/ browset events and their handlers
2. Forward-lookingL multitouch, gestures, acceleraometer
3. Non-standard UI & UX concepts
4. Cat herding - yanking it all together
5. Pushing the boundaries with experimentation

Unicorn - Full stack with UI/UX

Custom UI's require intimate knowledge of
1. HTML/CSS
2. LAyout & Positioning
3. Handling JS events
4. The order in which events fire
5. All the different kinds of events there are

 
Defensive Design (Nicholas Zakas)
Don't lose sight of what's right in front of you

DOM/ Browser events
	• Debounce
		• Scroll handler
		• Pointer Events
	• RequestAnimationFrame() - Get how many FPS to sync up animations/not call too many times
	• Late binding / ASAP unbinding
	• State-driven visual updates  - (JS) Polyfill access all inputs(mouse, touch, pen)
						 		   - (CSS as well) Can tell to not accept JS events
						 			• Can tell JS not to run (which might be too late) and handles it itself
	• Scioed contexts (keymage)	
		• For example, how Trello allows keyboard events to be different dependent on the page

Small wins:
	• Limit what you animate, when you animate, and how much
	• JANK: touchstart/mousedown events delay the compositor thread which draws to the screen

Managing a lot of corner cases and even bubbles
Multi-touch is a lot easier than you think
multi-touch event properties

What is binding??

Sense.js
Ball demo
Gyroscroll demo
Accelerometer - deviceorientation

event.alpha, beta, gamma

Non-standard UI & UX Concepts

	• Don't unleash revolutionary concepts without informing the user
	• Put a slight spin on standard apps
	• If the concept is not simple enough, developers can explain implementation, or prototypes & quality weren't given enough time to mature, it will fail
Once a UI problem is broken down into simple steps, figure out tools that will help you get you there (tougher)
• jQuery, Kendo, jQ

learn->adopt->master->unlearn->intuit

Shuhari (first learn, then detach & finally transcend)
• Find you "what ifs" & focus
• Prototype, start simple
• Deep focus -> intuition -> creativity -> problem solving -> delightful UIs


Start a new project as simple as it can get and only add things if you really need them (Stephen Hay)
BrowserAPIs 
labs.wit.ai (WEB SPEECH)

A note on performance
	• Animate as much as you can with declaritive CSS

Fat Finger
	• Fluff up event target with individual elements

Context-aware, not just responsive
DIY ethic
Strive for minimal animation code

Parallax battle
• Scrollfall
• VirtualScroll
• Regular ol' onScroll()
• Debounced game loop triggered on touch and on scroll
• CSS-only

Facing North - Touch/hold/drag radial menues

document.oncontectmenu = function() { return false }; document.ondragstart = function() { return false; };

HUD displays

Fantasy User Interfaces

GMUNK