# JavaScript going Vanilla, part 4 | Scope & Context

"Scope" and "Context" in JavaScript are 2 different things.

## Scope

* The body of the function
* Any variable defined here is not available on the "parent scope" / "outside the function"
* But they are available in all "children scopes" / "inner functions"
* !!! Lexical scope tree

## Context

* The "environment" where the function executes
* The context is always an object (or "undefined")
* The context is "this"

> It's possible to have 2 different functions having the same __context__

or

> It's possible to have 1 function that executes in 2 different __contexts__

## Who is _"this"_?new

* reserved word, available in all functions
* object (or "undefined")
* points to the function's current __context__
* takes different values, depending how the function is called

### Function form

```javascript
function foo() {
	console.log( this );
}
foo(); // global object (window)

function foo() {
	'use strict';
	console.log( this );
}
foo(); // undefined
```

### Method form

```
var o = {
	foo: function() {
		console.log( this );
	}
};
o.foo(); // [Object] o
```

### Constructor form

```
function Foo() {
	console.log( this );
};
var o = new Foo(); // [Object] o
```

### Call, Apply form

```javascript
var o = {
	foo: function() {
		console.log( this );
	}
};

var o2 = {};
o.foo.call( o2 ); // [Object] o2
```