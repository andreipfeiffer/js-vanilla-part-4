# JavaScript going Vanilla

by Andrei Pfeiffer

## Part 4: Scope & Context

"Scope" and "Context" in JavaScript are 2 different things.

### Scope

* Also called "Execution Context" in ECMAScript standards, which explains the confusion between the 2 terms
* Scope is actually a portion of code
* In JavaScript, scope is also named "lexical scope", or "static scope" because it gets evaluated and rendered at compile time
* Scope refers to variables visibility
  ```javascript
  // global scope
  var nr = 1;
  
  function parent() {
    // parent scope
    var nr = 2;
    
    function inner() {
    	// inner scope
    	var nr = 3;
    }
    
    inner();
  }
  
  parent();
  ```

* Any variable defined inside of a scope is not visible on the "parent scope" or "outside the function"
* But the same variable is available in all "descendant scopes" or "inner functions"
* So, inner functions contain the scope of the outer functions
* __Closures__ provide the same behavior even after the outer function has returned

### Context

* Called "ThisBinding" in the ECMAScript standards
* Can be refered to using "this" keyword
* The "environment" where the function executes
* The context is always an object
* It gets destroyed after it has executed all of the function's code

> It's possible to have 2 different functions having the same __context__

or

> It's possible to have 1 function that executes in 2 different __contexts__

### Who is _"this"_?

* reserved word, available in all functions
* object (or "undefined")
* points to the function's current __context__
* takes different values, depending how the function is called

#### Function form

When calling a simple function, it depends if ES5 '__strict mode__' is enabled or not. If it's enabled, the context will be set to `undefined`, otherwise it will reference the `window [Object]`, aka. the __global object__.

```javascript
function foo() {
	console.log( this );
}
foo();
// > global object (window)

function foo() {
	'use strict';
	console.log( this );
}
foo();
// > undefined
```

#### Method form

When calling a method from an object, it will always reference the object itself.

```javascript
var o = {
	foo: function() {
		console.log( this );
	}
};
o.foo();
// > [Object] o
```

#### Constructor form

Inside a Constructor, it will always reference the newly created object.

```javascript
function Foo() {
	console.log( this );
};
var o = new Foo();
// > [Object] o (the newly created Object)
```

#### Call, Apply form

To any function, or method, we can pass a custom context, using either `call` or `apply` methods.

```javascript
var o = {
	foo: function() {
		console.log( this );
	}
};

var o2 = {};
o.foo.call( o2 );
// > [Object] o2 (the specified Object)
```

#### Bind form

ES5 introduces a new method, that allow permanent binding of a custom context, to a function.

```javascript
var o = {
	foo: function() {
		console.log( this );
	}
};

var o2 = {};
var fuz = o.foo.bind( o2 );

fuz();
// > [Object] o2 (the specified Object)
```
