# Coding Practices

Styling uniformity is **vital** for coding efficiency. Therefore, follow this simple styling guide whenever adding, creating, or modifying files in this repository.

### In General

**Tabs for indentation**, spaces for alignment (see [this article][tabs and spaces article] for an explanation). While we're at it, always align—don't be bad.

Don't leave trailing whitespace! Most text editors have plugins that can make catching trailing whitespace easier (sublimetext has TrailingSpaces).

Avoid making lines too long, split into multiple lines if necessary. Also make sure your code is simple to understand, in 5 years you won't be here and someone else will need to maintain this, so **comments are necessary**.

### File System

There isn't any strict file-ordering system in place at the moment, but feel free to implement one (and modify this file).

Files should be named descriptively so that it's obvious what they are for, in hyphenated lowercase (Ex: default-event-list-header.html)

### HTML

It's very easy to just want to write messy HTML, but don't do it!

Put style tags above HTML and script tags below the HTML if you have them.

Tags in general should be hyphenated lower-case (class="event-description").

There should be empty lines before and after tag decelerations and closers, unless the tag only has one child tag and that tag has no children.

For example:

```html
<!-- This is fine -->
<tr>

	<div class="event-name">#_EVENTNAME</div>
	<div class="event-date">#_EVENTDATES</div>

</tr>

<!-- While the inner tags here have children of their own
     (the spans), it is clearly more legible to split up
     like this, so use your judgment if you are uncertain -->
<div class="event-details">

	<div class="event-description">
		<span class="desc-name">Description:</span> #_ATT{desc}
	</div>

	<div class="event-location">
		<span class="desc-name">Meet:</span> #_LOCATIONNAME (#_LOCATIONADDRESS) at #_EVENTTIMES
	</div>

</div>
```

Comment HTML when it is unclear. Not everyone understands HTML as well as you do, so put in comments. The styling for the comments themselves are up to you, there isn't any strict guideline for those.

**SEPERATE HTML AND CSS!!!** I cannot emphasize this enough. If you don't know how to do this, take a [quick lesson][codecademy html and css] in HTML and CSS! If separation into .css files is a hassle, just include a:

```html
<style type="text/css">

	/* formatting goes here */

</style>
```

on top. I know it's sub-ideal, but wordpress sucks. More on css later.

That being said, **avoid style tags ('style=...')**! These make the code much less maintainable, and makes it hell for future editors (I know from first-hand experience).

### CSS

All the tags (class, id, attributes eg: [name=user-name]) you are using should be in hyphenated lower-case.

Leave empty lines before start tags and after end tags:

```css
.css-events-list {
	text-align: center;
}

.css-events-list .event-name {
	color: #2182ab;
	font-family: Impact, Charcoal, sans-serif;
	font-size: -webkit-xxx-large;
	font-weight: bold;
	margin-bottom: 10px;
}

.css-events-list .event-date {
	color: #3f7e98;
	font-size: 36px;
	line-height: 57.59375px;
	font-weight: bold;
	text-decoration: underline;
	margin-bottom: 30px;
}
```

Be sure to make styles as specific as possible, using classes to select specific items (you want to be certain that it is never going to be applied to anything else).

Reuse styles as much as possible, avoid copy pasting styles into multiple places (maybe give all the elements a specific class with the shared styling). New stylers for some reason are obsessed with using id's instead of classes. That's good for javascript queries, but typically bad for styling (hard to reuse). Try also giving them a class and selecting them by class in the stylesheet, unless you are sure that you won't reuse the styling (if it's remotely possible, select by class).

I know some people also really care about the ordering of the style attributes within each style tag—if that's you feel free to update this file and the styling in the current stylesheets—but I personally don't really care, so do whatever.

### JavaScript

As a fellow JavaScript enthusiast myself, I know how hard it is to understand old code.

Naming is snakeCase in general, constants (const) should be written in uppercase characters separated by underscores (GOOGLE_FORMS_IFRAME_NAME) before all else. Use 'let' instead of 'var', learn the difference [here][let, const, and var].

For braces, follow [Google's braces format][google brace format]. Their formatting guide is good in general, it's a 10-20 minute read for when you get the chance.

```javascript
function myFunction() {
	let condition = true,
	    otherCondition = false;

	if (condition)
		doSomething();
	else if (otherCondition) {
		doSomethingElse();
		for (let i = 0; i < 15; i++)
			doSomethingSpecific(i);
	} else {
		elseSomethingDo();
	}
}
```

**AVOID JQUERY!** I know this is weird, I too started off using jQuery for everything, but then when I noticed how pathetically slow it was, I stopped. You'd be surprised at how easy it is to go back to javascript from jQuery. Ajax calls should still be with jQuery (for simplicity), but I doubt you'll need them.

**COMMENT WELL!!!!!!!!!!!!!!!!!!!!**
Not only should you name your variables and functions descriptively, comment your code whenever there is any ambiguity. Yes, I mean [JSDoc comments][jsdoc comments] whenever possible.

For example, do this:

```javascript
/**
 * Generates the Google Form with prefilled name.
 * @param  {String} name The full name of the user.
 */
function generateForm(name) {
	let iframeDiv = document.getElementById('rsvp-iframe-div'),
		iframeContent = GOOGLE_FORMS_IFRAME_NAME.format(name);
	iframeDiv.innerHTML = iframeContent;
}

// Although sometimes more detailed descriptions are necessary...

/**
 * Stores a key, item value pair as both in the localStorage
 * and as a cookie (cookies for mobile or whatnot).
 * for example:
 *
 * storeItem('tester', 123);
 * can be retrieved by:
 * getItem('tester');
 *
 * Note: Stores the items as JSON automatically, meaning
 * that they will maintain their data types (including
 * dictionaries!)
 * @param  {String} key   Key to store value as
 * @param  {any}    value Value to store for key
 */
function storeItem(key, value) {
	let jsonStringValue = JSON.stringify(value);
	localStorage.setItem(key, jsonStringValue);
	setCookie(key, jsonStringValue, 120 * 365);
}
```

It might seem silly for you, but make it a happen to comment your program after you get it to work; I find it relaxing myself.

Sometimes there's a fancy way to do things that's harder to understand for novel scripters. In that case, either do it and provide **solid** comments and a detailed explanation on how to use it, potentially modify it in the future, and how it works, or just do it in the simpler but easier to understand method.

Split up your functions into smaller functions, reuse your code as much as possible. *Your function length should be inversely proportional to its complexity.* Functions should rarely exceed 10 lines, and when they do make it something very simple, like a long switch statement, or a line of simple logic. This *rarely* happens though, so try enforcing the 10 line limit.

Try mimicking from existing javascript (I made a script tag in the bottom of single-event-page-format.html). Yes, this means that future Alephs will be mimicking you, so hold yourself to a high standard.

### Enjoy Programming!

Phew. Now that I got all of that out of the way, be sure to enjoy programming and to have fun and such!

Feel free to add on to this file, update outdated things, or modify it however you want. However, be sure to emphasize the importance of uniformity and of good practices.

For more information or comments, email me at: ofek@theofekfoundation.org

[tabs and spaces article]:http://lea.verou.me/2012/01/why-tabs-are-clearly-superior/ "tabs and spaces article"
[codecademy html and css]:https://www.codecademy.com/courses/web-beginner-en-HZA3b/0/1?curriculum_id=50579fb998b470000202dc8b "codecademy html and css lesson"
[let, const, and var]:https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75#.v34hkx1q0 "let vs const vs var"
[google brace format]:https://google.github.io/styleguide/javaguide.html#s4.1-braces "google brace format"
[jsdoc comments]:http://usejsdoc.org/about-getting-started.html "jsdoc comments"