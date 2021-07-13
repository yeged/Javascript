# Table of Contents

* [Types](#primitive-types)
  * [Coercion](#coercion)
  * [Boolean](#boolean)
  * [Equality](#equality)
* [Scope Closures](#scope)
  * [Function Scope](#function-scope)
  * [Block Scope](#block-scope)
  * [Undef vs Undec](#undef-vs-undec)
  * [Closure](#closure)
  * [Immutable vs Mutable](#immutable-vs-mutable)
* [Events, Async-Operations](#prevent-default)
  * [Bubble Capture Phase Stop Propagation](#bubble-capture-phase-stop-propagation)
  * [Bubbling](#bubbling)
  * [Capture Phase](#capture-phase)
  * [Stop Propagation](#stop-propagation)
  * [Async Operations](#async-operations)
  * [Promise](#promise)
  * [Async Await](#async-and-await)

# Javascript

## 1-) Types
* ###  Primitive Types

In JavaScript, a primitive (primitive value, primitive data type) is data that is **not an object and has no methods.** There are 7 primitive data types: string, number, bigint, boolean, undefined, symbol, and null.

All primitives are ***immutable***

* ###  Coercion 
````
Number + Number = Number

Number + String = String

String + Number = String

String + String = String
````
* ###  Boolean

|Truthy|Falsy|
|--|--|
|`"sample"`|`""`|
|`true`|`false`|
|`23`|`0`|
|`{}`|`null`|
|`!!"sample"`|`NaN`|
|`function test(){}`|`undefined`|

* ###  Equality
````
* 1 == "1" //true
* 1 === "1" // false
* null == undefined //true
* null === undefined //false
````
## 2-) Scope Closures

* ###  Scope

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

* ###  Undef vs Undec

````
var x;
console.log(x) // undefined

console.log(y) // undefined(undeclared)
````

* ###  Closure

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

* ###  Immutable vs Mutable

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

## 3-) Events, Async-Operations

* ###  Prevent Default

The preventDefault() method cancels the event if it is cancelable, meaning that the default action that belongs to the event will not occur.

Herhangi bir eventin varsayılan davranışını engellemek için kullanılır.
 
````
document.getElementById("submit").addEventListener("click", function(event){
  event.preventDefault()
});
````

* ###  Bubble Capture Phase Stop Propagation

https://codepen.io/yeged/pen/BaRLOWj

**HTML :**
````
<div id="grandparent" style="background-color: yellow; height: 450px; width: 450px;">
  GrandParent
  <div id="parent" style="background-color: purple; height: 300px; width: 300px;">
    Parent
    <div id="child" style="background-color: red; height: 150px; width: 150px;">
      Child
    </div>
  </div>
</div>
````

**View :**

![Ekran görüntüsü 2021-07-13 133255](https://user-images.githubusercontent.com/51911426/125437549-3bfcd39c-86af-470a-b05d-04b45521e365.png)

### Bubbling

Event bubbling is a method of event propagation in the HTML DOM API when an event is in an element inside another element, and both elements have registered a handle to that event. It is a process that starts with the element that triggered the event and then bubbles up to the containing elements in the hierarchy. In event bubbling, the event is first captured and handled by the innermost element and then propagated to outer elements


İç içe olan eventlerden event Handler'ı olan bir eleman tetiklendiğinde dışa doğru hiyerarşik bir şekilde event Handler'a sahip olan elemanları kabacrıklama(bubbling) ile yakalar.

**Javascript :**
````
let child = document.getElementById("child")
let parent = document.getElementById("parent")
let grandparent = document.getElementById("grandparent")

child.addEventListener("click", clickHandle)
parent.addEventListener("click", clickHandle)
grandparent.addEventListener("click", clickHandle)


function clickHandle(event){
  console.log('Clicked to -> ', this)
}
````

**Click Child Output :**

![12](https://user-images.githubusercontent.com/51911426/125438009-7aa3d53a-031b-428b-b226-733e52a870ff.png)

**Click Parent Output :**

![122](https://user-images.githubusercontent.com/51911426/125438144-cf66ef6f-ce92-47bd-a961-373e621a57be.png)

### Capture Phase

In event capturing, an event propagates from the outermost element to the target element. It is the opposite of event bubbling, where events propagate outwards from the target to the outer elements.

Dıştan içe doğru olur. Bir event capture edildiği zaman eventin sırası değişir. Bütün elemanlar capture edilirse default sırası dıştan içe olur. (Drag and Drop)

**Javascript :**

````
//addEventListener(eventName, handlerFunction, isCaptured)
isCaptured default : false

````

````
let child = document.getElementById("child")
let parent = document.getElementById("parent")
let grandparent = document.getElementById("grandparent")

child.addEventListener("click", clickHandle)
parent.addEventListener("click", clickHandle)
grandparent.addEventListener("click", clickHandle, true)


function clickHandle(event){
  console.log('Clicked to -> ', this)
}
````
**Click Child Output :**

![123](https://user-images.githubusercontent.com/51911426/125438526-f6d01ed8-bcba-4cd8-bab3-84a428275aad.png)

### Stop Propagation

Event flowunu durdurur. Tetiklendiği elemandan sonra bubble olmaz.

The stopPropagation() method of the Event interface prevents further propagation of the current event in the capturing and bubbling phases.
#### Stop Propagation on Child :

````
let child = document.getElementById("child")
let parent = document.getElementById("parent")
let grandparent = document.getElementById("grandparent")

child.addEventListener("click", clickChildHandle)
parent.addEventListener("click", clickParentHandle)
grandparent.addEventListener("click", clickGrandparentHandle)


function clickChildHandle(event){
  console.log('Clicked to -> ', this)
  event.stopPropagation();
}

function clickParentHandle(event){
  console.log('Clicked to -> ', this)
}

function clickGrandparentHandle(event){
  console.log('Clicked to -> ', this)
}
````
**Click Child Output :**

![124](https://user-images.githubusercontent.com/51911426/125439020-390e0d8c-d9a9-4bc0-b145-95aa160dcd23.png)

**Click Parent Output :**

![122](https://user-images.githubusercontent.com/51911426/125438144-cf66ef6f-ce92-47bd-a961-373e621a57be.png)

#### Stop Propagation on Parent :

````
function clickChildHandle(event){
  console.log('Clicked to -> ', this)
}

function clickParentHandle(event){
  console.log('Clicked to -> ', this)
  event.stopPropagation();
}

function clickGrandparentHandle(event){
  console.log('Clicked to -> ', this)
}
````

**Click Child Output :**

![12](https://user-images.githubusercontent.com/51911426/125439259-dcb12a0c-354f-4ed1-9178-d58ed64140dc.png)

**Click Parent Output :**

![12](https://user-images.githubusercontent.com/51911426/125439329-389444df-2b2b-43b0-9a6b-a119041f1b8a.png)

### Stop Propagation vs Prevent Default

It does not, however, prevent any default behaviors from occurring; for instance, clicks on links are still processed. If you want to stop those behaviors, see the preventDefault() method.

Prevent Default bir web elemanının default davranışını değiştirir. Browser'ın varsayılan davranışını engeller.

Stop Propagation Event flowun devam etmesini engeller.

* ### Async Operations

**HTML :**

````
<div>
  <button id="js-test">Test</button>
</div>
````

### XHR - Old Way Request

Closure sayesinde veri alındı ve asenkron bir işlem yapılmış oldu. Callback Yöntemi.


**Javascript :**
````
let button = document.getElementById("js-test")

button.addEventListener("click", () => {
  console.log("clicked!")
  function reqListener(event){
    const userInfo = JSON.parse(this.responseText) // Object
    console.log("User info :", userInfo.title)  
}
  var oReq = new XMLHttpRequest()
  oReq.open("GET", "https://jsonplaceholder.typicode.com/todos/1");
  oReq.addEventListener("load", reqListener)
  oReq.addEventListener("error", () => {
    console.log("sorry, error")
  })
  
  oReq.send()
  console.log("clicked end!")
});
````

**Output :**
````
>"clicked!"
>"clicked end!"
>"User info :" "delectus aut autem"
````

### Promise

Promisler birer objectdir. Pending -> Fullfill or Reject -> then -> return. 

**Fetch**

Fetch promise döndürür. Fetchden gelen bir promise result(Promise) döndürür.(Fullfill olduğunda response) Result json metodu döndürür ve başka bir promise döner. Zincirleme(Chain)

**Javascript :**
````
let button = document.getElementById("js-test")

button.addEventListener("click", () => {
  console.log("clicked!")
  fetch("https://jsonplaceholder.typicode.com/todos/1")
    .then(response => response.json())
    .then(json => console.log(json.title))
  console.log("clicked end!")
});

````
**Output :**
````
>"clicked!"
>"clicked end!"
>"User info :" "delectus aut autem"
````

**Vanilla Promise**

````
Resolve : then
Reject : catch
````
**Javascript :**
````
let button = document.getElementById("js-test")

const getUserFromStore = () => {
  const user = {title: "John"}
  // Reject("Noo")
  // return;
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(user)
    }, 100)
  })
}

button.addEventListener("click", () => {
  console.log("clicked!")
  getUserFromStore()
  .then((info) =>{            //Promise is fullfilled
    console.log(info.title)
  }).catch(() =>{
    console.log("some error")
  })
  console.log("clicked end!")
});
````

**Output :**
````
>"clicked!"
>"clicked end!"
>"John"
````

### Async and Await

Async keywordü herhangi bir fonksiyonu promise hale dönüştürmek için kullanılır. Promisler async operationslardır, asenkron çalışırlar. 

Await sırayla çalışır ve çalışana kadar bekletir. Bir sürü data çekerken loading işlemi gerçekleştirmek için kullanılabilir.

Async ise bir şeyleri asenksron yapar. Await bir şeyleri bekletir. Await bir üstteki satırı bekler. 

**Javascript :**
````
let button = document.getElementById("js-test")

const getUserFromStore = () => {
  const user = {title: "John"}
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(user)
    }, 2000)
  })
}

button.addEventListener("click", async () => {
  console.log("clicked!")
  const result = await getUserFromStore()
  console.log(result.title)
  console.log("clicked end!")
});

````

**Output :**
````
>"clicked!"
>"John"
>"clicked end!"
````

**Javascript :**
````
button.addEventListener("click", async () => {
  console.log("clicked!")
  const response = await fetch("https://jsonplaceholder.typicode.com/todos/1")
  const json = await response.json()
  console.log(json.title)
  console.log("clicked end!")
});

````

**Output :**
````
>"clicked!"
>"delectus aut autem"
>"clicked end!"
````

### Promise All ve Promise Any

Promise All : İçine verilen bütün asenkron operationlar bittiğinde çalışır sadece. Loading ekranı için işe yarar.

Promise Any : İçindekilerden sadece bir tanesinin bitmesini bekler.



