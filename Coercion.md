#### JSON Stringification
For most simple values, JSON stringification behaves basically the same as `toString()` conversions, except that the serialization result is *always a `string`*:
```js
JSON.stringify( 42 );	// "42"
JSON.stringify( "42" );	// ""42"" (a string with a quoted string value in it)
JSON.stringify( null );	// "null"
JSON.stringify( true );	// "true"
```
The `JSON.stringify(..)` utility will automatically omit `undefined`, `function`, and `symbol` values when it comes across them. If such a value is found in an `array`, that value is replaced by `null` (so that the array position information isn't altered). If found as a property of an `object`, that property will simply be excluded.
```js
JSON.stringify( undefined );					// undefined
JSON.stringify( function(){} );					// undefined

JSON.stringify( [1,undefined,function(){},4] );	// "[1,null,null,4]"
JSON.stringify( { a:2, b:function(){} } );		// "{"a":2}"
```
### Abstract Equality
#### Comparing: `string`s to `number`s
```js
var a = 42;
var b = "42";

console.log(a === b);	// false
console.log(a == b);		// true
```
***************

#### Comparing: `null`s to `undefined`s
```js
var a = null;
var b;

console.log(a == b); // true  
console.log(a === b); // false

console.log(b == null); // true
console.log(b === null); // false

console.log(b == undefined); // true
console.log(b === undefined); // true
```

#### Comparing: `object`s to non-`object`s

```js
var a = 42;
var b = [ 42 ];

console.log(a == b);	// true
```
```js
var a = "abc";
var b = Object( a );	// same as `new String( a )`

console.log(a === b);				// false
console.log(a == b);					// true
```

```js
var a = null;
var b = Object( a );	// same as `Object()`
console.log(a == b);					// false

var c = undefined;
var d = Object( c );	// same as `Object()`
c == d;					// false

var e = NaN;
var f = Object( e );	// same as `new Number( e )`
e == f;					// false
```
```js
var a = "abc";
var b = Object( a ); 
var c = Object( a ); 

console.log(c == b);     // false
console.log(a == null);  // false
console.log(b === undefined); // false
```
#### False-y Comparisons

```js
console.log("0" == null);			// false
console.log("0" == undefined);		// false
console.log("0" == false);			// true -- UH OH!
console.log("0" == NaN);				// false
console.log("0" == 0);				// true
console.log("0" == "");				// false

console.log(false == null);			// false
console.log(false == undefined);		// false
console.log(false == NaN);			// false
console.log(false == 0);				// true -- UH OH!
console.log(false == "");			// true -- UH OH!
console.log(false == []);			// true -- UH OH!
console.log(false == {});			// false

"" == null;				// false
"" == undefined;		// false
"" == NaN;				// false
"" == 0;				// true -- UH OH!
"" == [];				// true -- UH OH!
"" == {};				// false

0 == null;				// false
0 == undefined;			// false
0 == NaN;				// false
0 == [];				// true -- UH OH!
0 == {};				// false
```
```js
[] == ![];		// true

"" == [null];	// true

0 == "\n";      // true

"true" == true;                     // false
```
Let's look again at the *bad* list:

```js
"0" == false;			// true -- UH OH!
false == 0;				// true -- UH OH!
false == "";			// true -- UH OH!
false == [];			// true -- UH OH!
"" == 0;				// true -- UH OH!
"" == [];				// true -- UH OH!
0 == [];				// true -- UH OH!
```

Four of the seven items on this list involve `== false` comparison, which we said earlier you should **always, always** avoid. That's a pretty easy rule to remember.

Now the list is down to three.

```js
"" == 0;				// true -- UH OH!
"" == [];				// true -- UH OH!
0 == [];				// true -- UH OH!
```
## Abstract Relational Comparison

```js
var a = [ 42 ];
var b = [ "43" ];

a < b;	// true
b < a;	// false

```
However, if both values are `string`s for the `<` comparison, simple lexicographic (natural alphabetic) comparison on the characters is performed:

```js
var a = [ "42" ];
var b = [ "043" ];

a < b;                      // false -- string comparison!
Number( a ) < Number( b );  // true -- number comparison!
```

```js
var a = [ 4, 2 ];
var b = [ 0, 4, 3 ];

a < b;	// false
```

Here, `a` becomes `"4,2"` and `b` becomes `"0,4,3"`, and those lexicographically compare identically to the previous snippet.
```js
var a = { b: 42 };
var b = { b: 43 };

a < b;	// false
a == b;	// false
a > b;	// false

a <= b;	// true
a >= b;	// true
```
`a < b` is also `false`, because `a` becomes `[object Object]` and `b` becomes `[object Object]`, and so clearly `a` is not lexicographically less than `b`.
