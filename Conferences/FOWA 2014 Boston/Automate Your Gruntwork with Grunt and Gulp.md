Jason Lengstorf (Copter Labs) (ALSO, Boss)
@jlengstorf

Workflow Optimization 
	Task Runners - script that executes a list of actions, typically using one or more plugins
	Popular:
		Grunt
		Gulp
		Brunch
		Broccoli - really cool, look at it later

	We have a tendency to be lazy, inconsistent, forgetful, easily overwhelmed
	Robots are good at menial tasks
	Automation:
		• Spend less time "polish"
		• Less effort to do things right retroactively
		• Tasks are performed consistencies
		• Tasks are always completed


	Preprocessing:
		• LESS, SCSS, CoffeeScript, etc.
		• Concatenate & minify files (CSS & Javascript)
		• LINT files	- JSHint, JSLint
		• Start a server - for local development
		• Live reload changes- refresh browser when files change
		• Create production builds - output templates to static HTML, etc.
		• Optimize images - reduce the size of JPGs, PNGs, etc.
		• Bump File Versions - update package.json, bower.json, the Git versions
		• Pretty much anything

	Headache Gruntwork
		• Compile LESS to CSS
		• Add vendor prefixes to CSS
		• Lint JS Files
		• Combine and minify JS files
		• Set up a dev server locally
		• Reload when files are updated
		http://git.io/2JuyAA

	Vital Stats on Grunt.JS
	• Built on Node.js
	• Most popular task runner
	• Community is large
	• Thousands of available plugins

	INSTALL:

	• npm install grunt-cli --save
	• Create a gruntfile (Gruntfile.js) and save at the root of project

		module.export = function(grunt) 
		• Remember to install matchdep
	• For plugin installs:
		• npm install grunt-pluginname || npm install grunt-pluginname --save || npm install grunt-pluginname --save-dev
	• Select files that should be "grunted"
	• Compile less to css the hard way 
		• Client side (no, no, no)
		• Server-side (overkill in production)
		• Manually at deployment (a pain in the ass)
		• Use a third-party app like CodeKit (good, but...)
	CSS

	For grunt, use: npm install grunt-contrib-less --save-dev

	less: {
		dev: {
			options: {
				cleancss: true // minifies CSS output
			},
			files: {
				'arc/app/css/combined-grunt.min.css': 'src/app/less/{,*/}*.less'
			}
		}
	}

	VENDOR PREFIXES
		• Manually
		• LESS/SASS Mixins
		npm install grunt-autoprefixer --save-dev
		autoprefixer: {
			dev: {
				src: 'src/app/css/combined-grunt.min.css'
			}
		}

	REMOVE UNUSED CSS THE HARD WAY

	• npm install grunt-uncss --save-dev
	• Adds .unused to css file elements that are unused
	uncss: {
		testuncss: {
			files: {
			'demo/css/uncss-test-clean.css':'demo/index.html'
			}
		}
	}

	LINT JS FILES
	• To acoid non-issue errors, you can create a new file called .jshintrc
	• npm install grunt-contriv-jshint --save-dev


	• Put similar tasks under same name:
		grunt.registerTask('taskName', ['less:testname', 'js:testname'])

	UGLIFY (Minification)
		grunt-contrib-uglify

	DEV SERVER LOCALALLY
	npm install grunt-nodemon --save-dev

	nodemon: {
		dev: {
		`
		}
	}

	RELOAD:
		npm install grunt-contrib-watch --save-dev
		• Add configuration to Gruntfile

		Run nodemon and warch concurrently
		npm install grunt-concurrent --save-dev

	Register default task

	grunt.registerTask('default', [allTasks])


	GULP
	• Gulp is built on Node
	• Easier than Grunt
	• Little smaller than Gulp but helpful
	• Fewer plugins (but important ones are there)
	• Building custom plugins is less structured

	npm install gulp --save-dev

	gulp.task('styles', function() {
		gulp.src('app/less/main.less')
			.pipe(less({ cleancss: true })
			.pipe(prefix())
			.pipe(rename('combined-gulp.min.css'))
			.pipe(gulp.dest('app/css/'))
			.pipe(livereload())
		});
	}

	gulp.task('nodemon', function() {

	});

	• Watch is built-in
	• Register default task