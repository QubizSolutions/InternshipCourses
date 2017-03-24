# Introduction to TypeScript

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.
Any browser. Any host. Any OS. Open source.

TypeScript adds support for features such as classes, modules and an arrow function syntax as proposed in the ECMAScript 2015 standard.

## Primitive Types

Type | Code      
--- | ---
Any type (explicitly untyped) | `any`
void type (null or undefined, use for function returns only) | `void`
String | `string`
Number | `number`
Boolean | `boolean`

## Enum
```typescript
enum Options {
    FIRST,
    EXPLICIT = 1,
    BOOLEAN = Options.FIRST | Options.EXPLICIT
}
```

## Custom primitives. Type aliases

Type | Code      
--- | ---
Integer | `type int = number`
Float | `type float = number`

(!) The JS does not have types Integer and Float. It is only the type aliases. So you can make your code more documented and give a hint for programmers.


## Arrays

Concept | Code      
--- | ---
Array of strings | `string[]` or `Array<string>`
Array of functions that return boolean | `{() :boolean;}[]` or `Array<()=>boolean>`

## Tuples
A tuple is a finite ordered list of elements. A tuple in TypeScript is much like a typed list except that it is immutable (unchangeable) once created.

Concept | Code      
--- | ---
Tuple of list with first item number and second string | `let list :[number, string] = [123, 'abc'] `
or | `let list :Array<number, string> = [123, 'abc'] `

Tuple type
```typescript
type keyValuePair = [number, string];
let list :keyValuePair = [123, 'abc']
```

**Interface represents a tuple type**
```typescript
interface KeyValuePair extends Array<number | string> { 0: string; 1: number; }
```

## Functions

Concept | Code      
--- | ---
Function | `{ (arg1 :Type, argN :Type) :Type; }` or `(arg1 :Type, argN :Type) => Type;`
Constructor | `{ new () :ConstructedType; }` or `new () => ConstructedType;`
Function type with optional param | `(arg1 :Type, optional? :Type) => ReturnType;`
Function type with `rest` param | `(arg1 :Type, ...allOtherArgs :Type[]) => ReturnType;`
Function type with static property | `{ () :Type; staticProp :Type; }`
Default argument | `function fn(arg1 :Type = 'default') :ReturnType {}`
Arrow function | `(arg1 :Type) :ReturnType =>; {}` or `(arg1 :Type) :ReturnType =>; Expression`

## Arrows
Arrows are a function shorthand using the `=>` syntax.  They are syntactically similar to the related feature in C#, Java 8 and CoffeeScript.  They support both statement block bodies as well as expression bodies which return the value of the expression.  Unlike functions, arrows share the same lexical `this` as their surrounding code.

```JavaScript
// Expression bodies
var odds = evens.map(v => v + 1);
var nums = evens.map((v, i) => v + i);
var pairs = evens.map(v => ({even: v, odd: v + 1}));

// Statement bodies
nums.forEach(v => {
  if (v % 5 === 0)
    fives.push(v);
});

// Lexical this
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
}
```

## Generics

**Function using type parameters**

```typescript
<T>(items :T[], callback :(item :T) => T) :T[]
```

**Interface with multiple types**

```typescript
interface Pair<T1, T2> {
   first :T1;
   second :T2;
}
```

**Constrained type parameter**

```
<T extends ConstrainedType>() :T
```

## Generic type aliases
Type aliases requiring type parameters

```typescript
type Source<T> = T | (() => T);

function foo<T>(p: Source<T>) :T {
   return (typeof p === "function") ? p() : p;
}

// Usage:
foo<string>('abc');
foo<()=>number>(() :number => 123);
foo<()=>number>(function() :number { return 456 });
```

But compiler show error when using union type containing a function:
	
	Cannot invoke an expression whose type lacks a call signature.


**Type assertion**
```typescript
type Source<T> = T | (() => T);

function foo<T>(p: Source<T>) :T {
   return (typeof p === "function") ? (p as (()=>any))() : p;
}
```


## Type casting (assertion) and hinting

Concept | Code      
--- | ---
Call map() from type `a :string|string[]` | `(<string[]> a).map(s=>s.toUpperCase())`
... in JSX | `(a as string[]).map(...)`
Assertion for multi type `let v :string|number` | `parseInt( <string> v )`


## Dinamic type

Concept | Code
--- | ---
Dinamic type of any object | `type typeOfObject = typeof SomeObject;`

**Example**
```typescript
let Some = Math.round( Math.random() ) ? '' : 1;

type numOrStr = typeof Some;

let foo :numOrStr;
foo = 123;
foo = 'abc';
foo = {}; // Error!
```

## Interface

```typescript
 interface IChild extends IParent, SomeClass {
     property :Type;
     optionalProp? :Type;
     optionalMethod?(arg1 :Type) :ReturnType;
 }
 ```

## Classes
ES6 classes are a simple sugar over the prototype-based OO pattern.  Having a single convenient declarative form makes class patterns easier to use, and encourages interoperability.  Classes support prototype-based inheritance, super calls, instance and static methods and constructors.

```JavaScript
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }
  update(camera) {
    //...
    super.update();
  }
  get boneCount() {
    return this.bones.length;
  }
  set matrixType(matrixType) {
    this.idMatrix = SkinnedMesh[matrixType]();
  }
  static defaultMatrix() {
    return new THREE.Matrix4();
  }
}
```

## Template Strings
Template strings provide syntactic sugar for constructing strings.  This is similar to string interpolation features in Perl, Python and more.  Optionally, a tag can be added to allow the string construction to be customized, avoiding injection attacks or constructing higher level data structures from string contents.

```JavaScript
// Basic literal string creation
`In JavaScript '\n' is a line-feed.`

// Multiline strings
`In JavaScript this is
 not legal.`

// String interpolation
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`

// Construct an HTTP request prefix is used to interpret the replacements and construction
POST`http://foo.org/bar?a=${a}&b=${b}
     Content-Type: application/json
     X-Credentials: ${credentials}
     { "foo": ${foo},
       "bar": ${bar}}`(myOnReadyStateChangeHandler);
```

## Let + Const
Block-scoped binding constructs.  `let` is the new `var`.  `const` is single-assignment.  Static restrictions prevent use before assignment.


```JavaScript
function f() {
  {
    let x;
    {
      // okay, block scoped name
      const x = "sneaky";
      // error, const
      x = "foo";
    }
    // error, already declared in block
    let x = "inner";
  }
}
```
## Modules
Language-level support for modules for component definition.  Codifies patterns from popular JavaScript module loaders (AMD, CommonJS). Runtime behaviour defined by a host-defined default loader.  Implicitly async model – no code executes until requested modules are available and processed.

```JavaScript
// lib/math.js
export function sum(x, y) {
  return x + y;
}
export var pi = 3.141593;
```
```JavaScript
// app.js
import * as math from "lib/math";
alert("2π = " + math.sum(math.pi, math.pi));
```
```JavaScript
// otherApp.js
import {sum, pi} from "lib/math";
alert("2π = " + sum(pi, pi));
```

Some additional features include `export default` and `export *`:

```JavaScript
// lib/mathplusplus.js
export * from "lib/math";
export var e = 2.71828182846;
export default function(x) {
    return Math.log(x);
}
```
```JavaScript
// app.js
import ln, {pi, e} from "lib/mathplusplus";
alert("2π = " + ln(e)*pi*2);
```

## Reading

* https://johnpapa.net/es5-es2015-typescript/

## References

* https://github.com/lukehoban/es6features
* https://github.com/frontdevops/typescript-cheat-sheet/blob/master/README.md