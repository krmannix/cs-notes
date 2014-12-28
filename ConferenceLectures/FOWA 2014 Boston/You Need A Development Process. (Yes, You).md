Jason Lengstorf (Copter Labs) (ALSO, Boss)
@jlengstorf

Development Processes

	How we plan projects:
		Design
		Development
		QA
		Launch

	What really happens:
		Design
		Design
		Design
		Development
		QA/Launch

	This happened because we didn't have a proper process in plate:

	• What is a process?
		• Development processed are system or tools that remove bottlenecks in projects & make repetitive tasks automatic
	• What constitutes a process
		• Any task that will be repeated more than once should be treated as a process
	• Things that should be processes
		• The entire project workflow
		• Code generators or boilerplates
		• Code review - see what was changed and why
		• Repo management/branching
			• http://nvie.com/posts/a-successful-git-branching-model/
		• Design style guides/templates
			• Grid system
			• Common UI elements
	• Processes saves time
		• Solving problems that were already solved during a previous project is a huge waste of time and resources
	• Processes create clarity
		• A process eliminates questions of responsibility and project ownership
		• Do something, checkbox it, and then assign to someone else
		• Which helps avoid conflicts
		• Creating processes remoces the necessity and stress of making someone manually police day-to-day operations
	• Processes remove bottlenecks
		• If only one person in your organization knows how to solve your problem, you're focusing on the wrong problem

	The best PRocesses are automatic
		• Let a Task Runner handle development gruntwork
		• Use generators or boilerplates to start new products (YEOMAN)/Build your own
		• Use marcros to automate common responses (ZenDesk) - automatically sends out emails, etc. For example, if a client hasn't responded to a email in 48 hours, ZenDesk can send follow up emails automatically

	Make Common Processes Less Painful:
		• Don't write the same code twice:
			• If your compant works on one product, make reusable components into libraries or utility casses that can be shared
			• If your company works on client projects or multiple products without a shared codebase, keep reusable components available in a way that makese sense for your team
		• Create reusable messages
			• TextExpander
				• Code Snippets

	Creating a Process:
		1. Identify Similarities in Projects
			• Have we built something like this before
			• Can we reuse components from other projects
		2. Write down every step as a task
			• Don't make a task too general (ie: Build website)
			• LAyout sepcific expectations
Every step left open to interpretation is a potential point of failure
Expectations for what a "good job" is need to be extraordinarily clear
		3. Keep it Reasonable
			• In order to succeed, the process needs to be simpler to follow than the old approach
		Check "Slack"
		4. Put the process up for review
		5. Treat the process like the word of God
		6. Make adjustments as needed !!
			• ..But don't overtweak it. If a process needs to change every project it's not a process

	How to Ensure that Processes are followed:
		'Switch' - Chip & Dan Heath (READ THIS BOOK)
		7. Use a Tool Everyone "GETS"
		8. Follow the Process Yourself
		9. Make it painful not to follow
			• If they don't follow, make them do the same thing again
		10. Ask why it wasn't followed (if it wasn't)
			• If there are philisophical reasons, it is a coaching oppourtunity (this is how we do it here)

Processes can:
	• Help control chaos
	• Remove bottlenecks
	• Clarify expectations
	• Automate common tasks
	• Simplify development
	• Saves everyone time


Heroku + Orchestrate