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

### Function Scope

**var :**
````
console.log(x)
var x = 5
console.log(x)
````
**Hoisting**

````
var x;
console.log(x)
var x = 5
console.log(x)
````

**Output :**
````
> undefined
> 5
````

**Function**
````
sayHello()

function sayHello(){
	console.log("Hello")
}
````
**Hoisting**
````
function sayHello(){
	console.log("Hello")
}

sayHello()
````

**Output :**
````
> "Hello"
````
### Block Scope

**let :**
````
{
	let hello = "Hello";
}

console.log(hello)
````
**Output :**
````
Error: hello is not defined
````
or

````
console.log(hello)
let hello = "Hello";

````
**Output :**
````
Error: Cannot access 'hello' before initialization
````

**const :**
````
sayHello()

const sayHello = function(){
	console.log("Hello")
}
````
**Output :** 
````
Error: Cannot access 'sayHello' before initialization
````

## Undef vs Undec

````
var x;
console.log(x) // undefined

console.log(y) // undefined(undeclared)
````

## Closure

A closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

Fonksiyon değişkenlerinin fonksiyon bittikten sonra da erişebilir olması.


````
function number(n){
	console.log("begin")
  	setTimeout(function(){
    	console.log(n)
    },100)
  	console.log("end")
}

number(55)
````

**Output :**
````
> "begin"
> "end"
> 55
````
Function
````
function ask(fname){
	return function(lname){
    	console.log(fname, lname)
    }
}

const name = ask("Jane")

name("Doe")
````

**Output :**
````
> "Jane" "Doe"
````

## Immutable vs Mutable

Immutable.js

Keeping the state immutable can help you in terms of performance, predictivity and better mutation tracking.

WIth immutable entities, you can see the changes that happen to these objects as a chain of events. This is because the variables have new references which are easier to track compared to existing variables. 

Immutable tipler, mutable tiplerden daha performanslıdır. Yani daha hızlı çalışırlar. Çünkü önceki değer ile ilgili bir kontrol yapmaz ve veriyi direk ram’de bulduğu boş alana yazar. Performans kaygınız olduğunda bu tür durumları dikkate alarak uygulamanızda iyileştirmeler yapabilirsiniz

**Mutable**

Mutable is a type of variable that can be changed. In JavaScript, only objects and arrays are mutable, not primitive values.
````
let a = {name: "Jane"} // Memory : 123
let b = a // Memory : 123
a.name = "Joe" // Memory  : 123
console.log(a) // Joe
console.log(b) // Joe
````
**Immutable**
````
let a = "Jane" // Memory : 123
let b = a  // Memory 124
a = "Joe" // Memory 125 , Jane still in memory 123.
console.log(a) // Joe
console.log(b) // Jane
````
