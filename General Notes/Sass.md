<h1>Sass</h1>

<h3>Intro</h3>
* Originally written in Ruby, so can be installed via gem like 'gem install sass'
* To compile a Sass file, run `sass path/to/file.scss`
* To compile as we code, use `sass --watch path/to/folder`

* __Variables:__
`$color_name: #333;`
`$margin: 5px;`
* Can do Math on variables!
	* Make sure units are compatiable

* __@extend__
	* Can extend one selector to another
	* Similar to mix-in, but will just 'copy and paste' from one selector into another
	* Code would be .menu { @extend .bar };

* `%` (_placeholder_)
	* Create a 'class' that may not actually appear in CSS, but makes it easy to `@extend`

<h5>Nesting:</h5>

	.class {
		p {
			color: #ff0000;
		}
		a {
			font-size: 24px;
		}
	}

* _Advanced nesting:_
	* `&` is the advanced parent selector
		* Reverse order of nesting

	p {
		font-size: 12px;
		html.csscolumns & {
			column-count: 2;
		}
	}

	a {
		&:hover {
			color: blue;
		}
	}

	* `>` direct descendent (gets first child)

<h5>Color Functions</h5>
* lighten
	* Lightens a color by a certain percentage
	* `lighten($text-color, 20%)`

* darken
	* Darkens a color by a certain percentage
	* `darken($text-color, 10%)`

* complement
	* Outputs the complement of a color
	* complement($background-color)

* desaturate
	* desaturate(#345, 20%);

<h5>Mixins</h5>
* A way to group and distribute attributes for reuse

	@mixin roundy {
		border-radius: 4px;
	}
	@mixin green-links {
		a {
			color: green;
		}
	}

	.box {
		@include roundy;
		@include green-links;
	}

* Can pass arguments into mixins!

	@mixin roundy($radius-one) {
		border-radius: $radius-one;
	}

	.box {
		@include roundy(4px);
	}

<h5>Importing</h5>
* If there's an underscore at the beginning of the file, it won't automatically compile it
* `@import "_variables.scss";`
	* We can bring in elements from other scss files into the current one
* There is usually a _globals.scss_ file
* This order works:
	1. Define variables
	2. Global styles
	3. Page specifics
* Importing is good for using a __"reset CSS"__ file

<h5>Libraries</h5>
* Bourbon & Compass are both good libraries that allow for abstraction of vendor-prefix code

<h5>Functions</h5>
* red/blue/green
	* Return the values for r, g, or b for a color
* unquote()
	* Removes the quotes from a string
* `@function fn_name($value) { @return $value + 5;}`

<h5>Media Queries</h5>

	@media (max-width: 480px) {
		a {
			// Other stuff			
		}
	}

can become

	a {
		@media (max-width: 480px) {
			// Other stuff
		}
	}

<h5>Interpolation & If/Else</h5>
* `#{$value}` is replaced by the `$value` when we're trying to dynamically change the selector
* We can do the same within quotes "#{$value}"
* @if $value == red { border: 1px solid black } @ else if { color: green } @ else { color: blue }

<h5>Loops</h5>
* __@for__
	@for $i from 1 through 100 {
		.box:nth-child(#{$i}) {
			background: darken(white, $i)
		}
	}

* __@each__
	@each member in thom, johnny, phil, kevin {
		.bandmember.#{$member} {
			background: url("images/#{$member}.jpg");
		}
	}

<h5>Advanced Mixins</h5>
* __Lists:__
	@mixin band($members...) {
		for each $member in $members {
			.#{$member} {
				background: url("images/#{$member}.jpg");
			}
		}
	}

* Can call this with `@include band(kevin john kyle alex brian);
	* __No Commas!!__

* __Order of arguments:__
	@mixin box($color, $size) {
		width: $size;
		color: $color;
	}

* Can call with `@include box($color: blue, $size: 10px);`


* __Default values:__
	@mixin box($color: blue, $size) {
		width: $size;
		color: $color;
	}

* Can call with `@include box($size: 10px);

