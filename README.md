# Javascript

## 1-) Types
### Primitive Types

In JavaScript, a primitive (primitive value, primitive data type) is data that is **not an object and has no methods.** There are 7 primitive data types: string, number, bigint, boolean, undefined, symbol, and null.

All primitives are ***immutable***

### Coercion 
````
Number + Number = Number

Number + String = String

String + Number = String

String + String = String
````
### Booelan

|Truthy|Falsy|
|--|--|
|`"sample"`|`""`|
|`true`|`false`|
|`23`|`0`|
|`{}`|`null`|
|`!!"sample"`|`NaN`|
|`function test(){}`|`undefined`|

### Equality
````
* 1 == "1" //true
* 1 === "1" // false
* null == undefined //true
* null === undefined //false
````
## 2-) Scope Closures

### Scope

|Function Scope (Hoisting) |Block Scope|
|--|--|
|`var x; `|`let x;`|
|`function test(){}`|`const x = function(){}`|




