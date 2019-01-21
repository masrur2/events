# Events [![Build Status](https://travis-ci.org/cferdinandi/events.svg)](https://travis-ci.org/cferdinandi/events)
A tiny (700kb minified and gzipped) event delegation helper library.

Events lets you setup individual event listeners throughout your code, but runs them all in a single event listener behind-the-scenes. [Learn more about why you should use event delegation.](https://gomakethings.com/checking-event-target-selectors-with-event-bubbling-in-vanilla-javascript/)

[View the Demo](https://codepen.io/cferdinandi/pen/gqYrbe)


<hr>

### Want to learn how to write your own vanilla JS plugins? Check out my [Vanilla JS Pocket Guides](https://vanillajsguides.com/) or join the [Vanilla JS Academy](https://vanillajsacademy.com) and level-up as a web developer. 🚀

<hr>


## Installation

Compiled and production-ready code can be found in the `dist` directory. The `src` directory contains development code.

There are two versions of Events: the standalone version, and one that comes preloaded with a polyfill for `closest()`, which is only supported in newer browsers.

If you're including your own polyfills or don't want to enable this feature for older browsers, use the standalone version. Otherwise, use the version with polyfills.

**Direct Download**

You can [download the files directly from GitHub](https://github.com/cferdinandi/events/archive/master.zip).

```html
<script src="path/to/events.polyfills.min.js"></script>
```

**CDN**

You can also use the [jsDelivr CDN](https://cdn.jsdelivr.net/gh/cferdinandi/events/dist/). I recommend linking to a specific version number or version range to prevent major updates from breaking your site. Smooth Scroll uses semantic versioning.

```html
<!-- Always get the latest version -->
<!-- Not recommended for production sites! -->
<script src="https://cdn.jsdelivr.net/gh/cferdinandi/events/dist/events.polyfills.min.js"></script>

<!-- Get minor updates and patch fixes within a major version -->
<script src="https://cdn.jsdelivr.net/gh/cferdinandi/events@1/dist/events.polyfills.min.js"></script>

<!-- Get patch fixes within a minor version -->
<script src="https://cdn.jsdelivr.net/gh/cferdinandi/events@1.0/dist/events.polyfills.min.js"></script>

<!-- Get a specific version -->
<script src="https://cdn.jsdelivr.net/gh/cferdinandi/events@1.0.0/dist/events.polyfills.min.js"></script>
```



## The API

### `on()`

Add an event listener.

```js
/**
 * Add an event
 * @param  {String}   types    The event type or types (space separated)
 * @param  {String}   selector The selector to run the event on
 * @param  {Function} callback The function to run when the event fires
 */
events.on(types, selector, callback);
```

**Example**

```js
events.on('click', '.sandwich', function (event) {
	var filling = event.target.getAttribute('data-sandwich-filling');
	console.log(filling);
});
```

You can attach the same callback to multiple event types or selectors by separating them with a comma.

```js
// Attach to multiple events
events.on('click, input', '.sandwich', myCallback);

// Attach to multiple selectors
events.on('click', '.sandwich, .tuna, .turkey', myCallback);
```

### `off()`

Remove an event listener. All three arguments must be identical to the ones used when setting up the listener.

```js
/**
 * Remove an event
 * @param  {String}   types    The event type or types (space separated)
 * @param  {String}   selector The selector to remove the event from
 * @param  {Function} callback The function to remove
 */
events.off(types, selector, callback);
```

**Example**

```js
events.off('click', '.sandwich', function (event) {
	var filling = event.target.getAttribute('data-sandwich-filling');
	console.log(filling);
});
```


## Selectors

You can pass in any valid CSS selector (or combination of selectors). Events uses `closest()` under-the-hood to check if the element that triggered the event matches the selector (or is inside an element that does).

```js
// ID as a selector
events.on('click', '#turkey', myCallback);

// Data attribute selector
events.on('click', '[data-sandwich="turkey"]', myCallback);

// Multiple selectors
events.on('click', '.turkey, .tuna, .ham', myCallback);
```

To run your callback on any element, pass in `*` for a selector.

```js
events.on('click', '*', myCallback);
```

You can also pass in a node instead of a selector string.

```js
var sandwich = document.querySelector('.sandwich');
events.on('click', sandwich, myCallback);
```



## Working with the Source Files

If you would prefer, you can work with the development code in the `src` directory using the included [Gulp build system](http://gulpjs.com/). This compiles, lints, and minifies code.

### Dependencies
Make sure these are installed first.

* [Node.js](http://nodejs.org)
* [Gulp](http://gulpjs.com) `sudo npm install -g gulp`

### Quick Start

1. In bash/terminal/command line, `cd` into your project directory.
2. Run `npm install` to install required files.
3. When it's done installing, run one of the task runners to get going:
	* `gulp` manually compiles files.
	* `gulp watch` automatically compiles files when changes are made and applies changes using [LiveReload](http://livereload.com/).



## Browser Compatibility

Events works in all modern browsers, and IE 9 and above.

### Polyfills

Support back to IE9 requires a polyfill for the `closest()` method. Use the included polyfills version of Events, or include your own.



## License

The code is available under the [MIT License](LICENSE.md).