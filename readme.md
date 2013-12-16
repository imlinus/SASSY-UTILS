# SASSYUTILS

Our utilities to help us speed up our SCSS development.

## Index
* Prelude
* How to use

	* Placehold
	* globals.scss
	
* Utilities
	
	* all-keyframes
	* all-prefix
	* alpha
	* animation
	* arrow
	* background-cover
	* clearfix
	* columns
	* ellipsis
	* font-face
	* font-smoothing
	* inline-block
	* ir
	* positioning
	* rem
	* respond
	* sprite
	* transition
	* user-select
	* vertical-center
	
* Vertical rhythm

## Prelude
These utilities are made to help us develop quicker and easier, to keep our SCSS code clean and DRY.

It's built to handle "all" repetitive code in our stylesheets, by stacking attributes that goes "hand in hand" together, all prefixed and ready for production.

## How to use
This is utilities that will help speed up your development, you choose what you want to use and how you want to use it. Just use a few, or use them all. Whatever feels best.

#### Placehold
A thumb rule that I try to follow is that if it's a `@mixin` without arguments — then placehold it. (`%`)

All utilities are mixins, that we then later placehold if it's without arguments so that you can call it within media-querys (where `@extend` unfortunately doesn't work).

When working outside of media-querys, **ALWAYS** use placeholders to keep the generated css free from bloat.

In SCSS you can't `@extend` within a media-query. That's why we always have them as mixins, even if they're "only" used as placeholders, that day might come when you need to call it within a media-query, and then you're happy you can `@include` it as well.

#### globals.scss
Your globals file is the file where you keep all your settings. Keep this clean and modify it for your needs.

It's in here where we set our base font-size and line-height (if you're going to use `rem`'s), we also set the preferred media-query screen sizes in here.

The `globals.scss` file is also the file where you should stack your colors, sizes, z-indexes and pre set transitions.

## Utilities

* all-prefix
* alpha
* animation
* arrow
* background-cover
* clearfix
* columns
* ellipsis
* font-face
* font-smoothing
* inline-block
* ir
* keyframes
* positioning
* rem
* respond
* sprite
* transition
* user-select
* vertical-center

#### All Prefix
Handles all vendor-prefixing. Prefixes to selected attribute.

You can change the prefixes on line 9 in `globals.scss`, default is `-webkit-`, `-moz-` & `-ms-`.

This is mostly used within other mixins, but it can come handy for some attributes that needs vendor-prefixing.

	.ball {
	  width: 20px;
	  height: 20px;
	  @include prefix(border-radius, 10px);
	}

#### Alpha
Alpha mixin for cross-browser transparency.

Placeholders: `%alpha-0`, `%alpha-50`, `%alpha-100`

	.alpha-box {
	  background: red;
	  @include alpha(.5);
	  
	  // or one of the pre set
	  @extend %alpha-50;
	}

#### Animation
Mixin for calling animations, cross-browser prefixed.


	.bg {
	  width: 100%;
	  height: 640px;
	  @include animation(animation .5s ease-in-out);
	}

#### Arrow
Mixin for creating css arrows, neat little mixin that handles all the ugly code in a very stylish way.

`@include arrow(direction, color, size);`

Available directions: `top`, `right`, `bottom`, `left`, `top-left`, `top-right`, `bottom-left`, `bottom-right`

	.arrow {
	  @include arrow(top-left, #000, 15px);
	}

#### Background-cover
The `background-size: cover;` attribute in css is a tricky one due to that it needs special hacks for IE.

No problems, let's crunch it up as a mixin we can call instead!

	body {
	  @include background-cover('path/to/background.jpg');
	}

#### Clearfix
When building a layout with `float`s, the clearfix is a handy little snippet every developer knows about. Now also as placeholder/mixin.

	#main {
	  @extend %clearfix;
	  
	  // or within MQ's
	  @include clearfix;
	}


#### Columns
Css columns is a great new attribute to css3. Making columns becomes an ease, but be careful, this doesn't work in *IE9 or below*

	#main {
	  @include column-count(2); // two columns
	  @include column-gap(40px); // with 40px gap
	}
	
#### Ellipsis
If the text is too long, and you need it to ellipse (…), use this placeholder/mixin.

	#sidebar p {
	  @extend %ellipsis;
	  
	  // or within MQ's
	  @include ellipsis;
	}

#### Font-face
When using custom web fonts, use this mixin to import the new font *(works down to IE8)*

	@include font-face(
	  'icomoon',
	  font-files(
	    "icomoon.woff",
	    "icomoon.svg"
	  ),
	  "icomoon.eot"
	);
	
	@mixin icomoon {
	  font: { family: 'icomoon', sans-serif; }
	}

Create a mixin for the new typo, and call the mixin wherever you need the font!

	%icon {
	  width: 20px;
	  height: 20px;
	  @include icomoon;
	}


#### Font-smoothing
New css3 attribute, `font-smoothing`. As mixin with (future-set) prefixing.

Use: `antialiased`, `subpixel-antialiased` or `none`

	body {
	  @include font-smoothing(antialiased);
	}

#### Inline-block
Cross-browser `inline-block` is really messy. fortunately for us when combined to a mixin and extended as an placeholder, inline block becomes as easy to use as it should be!

	.menu-item {
	  @extend %inline-block;
	  
	  // or within MQ's
	  @include inl-block;
	}

#### IR
Hiding text behind images is necessary in order to keep Google and other search engines pleased. There's hundreds of different techniques for archiving this. Here's one of the most popular ways ready to use

	.logotype {
	  background: url('path/to/logotype.png');
	  @extend %ir;
	  
	  // or within MQ's
	  @include ir;
	}

#### Keyframes
Mixin for easily creating and managing keyframes. keep all your keyframes within the `_keyframes.scss` file.

	@include keyframes(animation) {
	  0% { background: red; }
	  50% { background: green; }
	  100% { background: blue; }
	}
	
	
#### Positioning
Positioning in CSS always means at least a couple of attributes, let's combine all the repetitive code and make our positioning an ease.

`relative`, `absolute`, `fixed` or `static`

	@include position(position, top, right, bottom, left);
	
	.absolute {
	  width: 100%;
	  height: 50px;
	  @include position(absolute, 0px, 0px, null, 0px);
	}

#### REM
This is a mixin by [Ryan Frederick](https://github.com/ry5n/rem) that I've extended to some of the most common attributes in css.

REM is a new, better way for sizing, but IE8 needs pixel fallback. That's what this mixin does, provides a fallback for internet-explorer.

Mixins ready for usage is:

* `margin`
* `margin-top`
* `margin-right`
* `margin-bottom`
* `margin-left`
* `padding`
* `padding-top`
* `padding-right`
* `padding-bottom`
* `padding-left`
* `text-indent`
* `width`
* `min-width`
* `max-width`
* `height`
* `min-height`
* `max-height`
* `font-size`
* `line-height`

Along with two helper functions that you can call, `rem-calc()` & `px-calc()`

	blockquote {
	  border-left: px-calc(.25rem) #000 solid;
	}
	  
	@include margin(1.5rem 1rem .5rem 1rem);
	
	@include margin-left(1.5rem);
	
	@include text-indent(1.5rem);
	
#### Respond
A set of ready media-querys. Default-sizes is `480px`, `768px` & `1024px` but you can easily change that in the `globals.scss` file.

Media-querys ready for use is:

 * `desktop`
 * `tablet`
 * `mobile`
 * `retina`
 * `portrait`
 * `landscape`
 * `print`
 
 Use like you always use MQ's in SCSS
 
 	.box {
 	  width: 50px;
 	  height: 50px;
 	  
 	  @include respond(mobile) {
 	  	width: 25px;
 	  	height: 25px;
 	  }
 	}

#### Sprite
This mixin allows you to generate sprites "on the fly", with retina-support.

Simply create two images with the same name, one twice as big as the original. Then drop your images in the `sprites/` & `sprites-retina/` directories and call for your image without the `.png` extension.

The images has to be `.png`s

	.avatar { 
	  @include sprite(no-avatar);
	}

#### Transition
Mixin for calling transitions, cross-browser prefixed.

Tip: pre-define your transitions in your `globals.scss` file as variables.

	.comment-link {
	  @include transition($default-page-transition);
	}

#### User-select
When text needs to be unselectable, use this placeholder/mixin.

If used as mixin, you can either use: `none`, `text` or `all`.

	.toolbox {
	  @extend %user-select-none;
	  // or
	  @include user-select(none);
	}

#### Vertical-Center
Archiving vertical center in CSS can be hard. It depends if you know the size and width or not, if you need to support IE or not.

There's a couple of different methods for completing this task, choose the one that fits you best!

##### Technique 1
Requires a declared `height` and `width`. And `position: relative` on parent element.

	.box {
	  height: 50%;
	  width: 50%;
	  @include vertical-center-1;
	}

##### Technique 2

Same for this mixin, also requires `width` and `height`. And `position: relative` on parent element.

	.box {
	  width: 400px;
	  height: 200px;
	  @include vertical-center-2(400px, 200px);
	}

##### Technique 3

This mixin archives vertical centering via `transform: translate`, and **does not work in IE**.

	.box {
	  @include vertical-center-3;
	}


##### Technique 4

This doesn't require any width or height, but it requires some *extra markup*.
It works in almost all browsers (even IE7).

	.wrapper {
	   @include vertical-center-4;
	}
	
	 <div class="wrapper">
	   <div class="content">
	     <div class="box">
	       <!-- content here -->
	     </div>
	   </div>
	 </div>

## vertical rhythm
There's a vertical rhythm grid that can be toggled for view in `globals.scss` on line 3.

	$grid: false !default; // set to true for vertical rhythm grid
