[![Build Status](https://travis-ci.org/jdarling/Object.observe.svg?branch=master)](https://travis-ci.org/jdarling/Object.observe)

NOTICE
==============

This repo is now deprecated. The project has moved to https://github.com/ellipticaljs/Object.observe

Forked Status
=============
While there is no direct support for Array.observe, arrays passed to the Object.observe shim will now produce change records in the callback that match
the current stable Chrome 46 build for type "splice" in the accept list(which is the default).


Forked Modifications
====================

    * Converted to a UMD Module
    * Added Object.observe "splice" support for arrays
    * Removed SetImmediate
    * Removed "Use Strict" statement
    * Gulp Build Tasks
    * Bower Package
    
    

Object.observe Polyfill/shim
============================
Thanks to my new job I have a lot more time to devote to things like this library.  It has gone a REALLY long time without updates and there is a lot that can be done to make it more functional.  I hope to be spending more time on it soon, but for now I've fixed all the bugs that I know of and have been reported.  Thanks to everyone for their reports, and keep them coming if you find one.

Started as GIST: https://gist.github.com/4173299

Tested against Chromium build with Object.observe and acts EXACTLY the same for the basics, though Chromium build is MUCH faster.

Trying to stay as close to the spec as possible, this is a work in progress, feel free to comment/update

http://wiki.ecmascript.org/doku.php?id=harmony:observe




Limits so far
--------------
  Built using polling in combination with getter&setters.  This means that if you do something quick enough it won't get caught.

  Example:
```js
var myObject = {};
Object.observe(myObject, console.log);
myObject.foo = "bar";
delete myObject.foo;
```

  The observer function would never see the addition of foo since it was deleted so quickly.
  
  Additional limit: Overriding the accept list w/o "splice" will produce change records that will not match the current Chrome stable(38) if an array is passed to Object.observe.
  
  

Testing
-------

To run the tests first make sure you have Node.js installed.  Then use NPM to install Karam and all dependencies:

```
npm install
```

Finally run the tests with:

```
npm test
```

Planned Updates
---------------
  For FireFox using Proxies will result in better performance.  Will look into this more.

Examples and Usage
------------------
  See examples folder

Latest Updates
--------------

    * Memory leak fixed with PR #16
    * Tests added to project thanks to mikeb1rd also part of PR #16
    * Added Notifier.notify() with custom types support by klimlee
    * Added accept list support by klimlee
    * Stopped monitoring DOM nodes, Canary can't do it and neither should the shim.
    * Added in support for setImmediate if it is available.
    * Memory leak fix by Moshemal
    * Array length now reports as an update when it changes
    * Added enumerable flag to defineProperty


    
