#Timed

Timed provides syntactic sugar around JavaScript's native 
`setTimeout` and `setInterval` functions.

To execute some code in 5 minutes, instead of writing:

```js
setTimeout(function() { ... }, 300000); // how many zeros is that?
```

or the slightly more readable:

```js
setTimeout(function() { ... }, 5 * 60 * 1000); // 5... (multiplies in head) min
```

now you can just write:

```js
Timed.after(5, "minutes", function() { ... });
````

`setTimeout` becomes `Timed.after` and `setInterval` becomes `Timed.every`.

.every() and .after() both return a timer object which contains the calculated interval, a reference to the callback, the setTimeout/setInterval handle, and two control functions:

- `timer.cancel()`: Cancels the timer and nulls timeout id.
- `timer.start()`: Restarts the timer after it has been canceled, using the same callback as before.

These two functions both return `this` to allow for chaining.

###.yield()

Timed also provides a simple function yield processing time to the browser before executing the next block of code.

```js
Timed.yield(function() { ... });
```

This takes advantage of the `window.postMessage()` feature (when available) to execute the block as soon as the browser hands control back to JavaScript, often yielding faster results than a setTimeout can.  In older browsers, .yield() falls back to a 0 millisecond timeout.

##Usage

These are all valid calls:

```js
Timed.after(100, function() { ... });           // 100 milliseconds
Timed.after("9.7", function() { ... });         // 9.7 milliseconds
Timed.after("50sec", function() { ... });       // 50 seconds
Timed.after(7, "mins", function() { ... });     // 7 minutes
Timed.after("33", "hours", function() { ... }); // 33 hours
Timed.after("2 hours, 45 minutes", function() { ... }); // 2 hours, 45 minutes
Timed.after("minute", function() { ... });      // 1 minute
Timed.after([
	["1", "minute"],
	[34, "seconds"],
	"100 milliseconds"
], function() { ... });
```

`Timed.every`, for creating intervals, has the same exact syntax as `$.after`.

Valid time units include:  

* millisecond(s) (default)
* ms

* second(s)
* sec(s)
* s

* minute(s)
* min(s)
* m

* hour(s)
* hr(s)
* h

* day(s)
* d

##noConflict & jQuery

Timed supports calling the `.noConflict()` function to remove the Timed namespace.  `noConflict()` will then return the Timed object for assignment to a new location.

If you wish to remap Timed's functions into jQuery's global object it can be done like so:

```js
    $.extend($, Timed.noConflict());
```


##Meta

_Licensed under the 3-clause **BSD license** (BSD_LICENSE.txt)_

Copyright (c) 2011, Jarvis Badgley (chipersoft at gmail), Arthur Klepchukov (at gmail)
