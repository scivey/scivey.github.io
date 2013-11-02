title: "Background: Partial Application and Currying"
tags: partial, functional, underscore, curry, spice, delicious, application, lodash, function
synopsis: "Background for other articles: a review of the basic functional programming concepts of partial application and currying."

--- 

This article is intended as background for other articles on this site, as many of them use partial application.

####Partial Application

Partial application is a higher-order operation which takes a function of two or more parameters and returns a copy of that function with at least one of those parameters bound ("filled in").  The `partial` function below is a very simple implementation of such an operation.  It assumes that any function passed to it has exactly two parameters, and that exactly one of those will be provided for binding.  Further down the page, we'll examine more generally useful implementations.

```javascript

// funcRef is a reference to another function, which takes two parameters
var applyPartial = function(funcRef, firstParam) {
	return function(secondParam) {
		return funcRef(firstParam, secondParam);
	}
}

var multiply = function(x, y) {
	return x * y;
}

var multByTen = applyPartial(multiply, 10);

multByTen(6.5); // 65
```

Unless a direction is specified, partial application generally refers to filling in a function's parameters from left to right.  Partial application from the right is also useful in some circumstances:

```javascript

// funcRef is a reference to another function, which takes two parameters
var applyRightPartial = function(funcRef, secondParam) {
	return function(firstParam) {
		return funcRef(firstParam, secondParam);
	}
}

var divide = function(x, y) {
	return x / y;
}

var divideBy6 = applyRightPartial(divide, 6);

divideBy6(72); // 12
```

What about functions of more than two parameters?  Partial application can also be very helpful here, but the implementation looks slightly awkward.  The basic problem is  determining when to invoke the original function.  In many languages a given function has a fixed number of parameters which must be supplied (i.e. a type signature), but Javascript has _variadic_ functions which accept any number of parameters.
