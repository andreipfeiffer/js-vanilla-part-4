# JavaScript going Vanilla

by Andrei Pfeiffer

## Part 4: Scope & Context

"Scope" and "Context" in JavaScript are 2 different things.

### Scope

* The body of the function
* Any variable defined here is not available on the "parent scope" / "outside the function"
* But they are available in all "children scopes" / "inner functions"
* !!! Lexical scope & closures

### Context

* The "environment" where the function executes
* The context is always an object (or "undefined")
* The context is "this"

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
