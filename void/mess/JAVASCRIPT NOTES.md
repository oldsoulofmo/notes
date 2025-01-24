# Data structures, modern operators and strings
### Destructuring arrays 

	Destructuring assignment is a special syntax that allows us to “unpack” arrays or objects into a bunch of variables, as sometimes that’s more convenient. 

A great example with _split_ :

```javascript
let [firstName, surname] = "John Smith".split(' ');
alert(firstName); // John
alert(surname); // Smith
```

	Destructuring assignment works by iterating over the right value, the right of = and then assigns value for the left value (of =).

Ignoring unwanted values from an array can be so useful : 

```javascript
const array = ["john","wick","shit"];
const [name,,adjective] = array;

// name = john 
// adjective = shit
```

Looping with `.entries()`

```javascript
let user = {
  name: "John",
  age: 30
};

// loop over keys-and-values
for (let [key, value] of Object.entries(user)) {
  console.log(`${key}:${value}`); // name:John, age:30
}
```

Swap variables : 

```javascript
let guest = "Jane";
let admin = "Pete";

// Let's swap the values: make guest=Pete, admin=Jane
[guest, admin] = [admin, guest];

alert(`${guest} ${admin}`); // Pete Jane (successfully swapped!)
```

The rest (`...`) 

	If the array is too and we to destruct it into chosen variables then the rest of the array is omitted. 

```javascript
const names = ["jane","joe","james","benzema","zidane","carlos","jasmine"];
let [admin1, admine2, ...users] = names;
// admin1 = jane 
// admin2 = joe 
// users[0] = james 
.
.
.
// users[5] = jasmine
```

#### Default values 

	Default values can be more complex expressions or even function calls. They are evaluated only if the value is not provided.

An example that prompts to enter the last name if not provided in the array already : 

```javascript
let [firstName = "shit", lastName = prompt('your last name ?')] = ["mohammed"];
console.log(firstName,lastName);

// firstName : mohammed 
// lastName : It gets the default value which will be enter by the user 
```

### Object destructuring

We can surely use defaults and name variables as we wish !

```javascript
const shit = {
  title: "warzone",
  type: "video game",
  year: 2010,
};

const shit2 = {
  title: "fifa",
  year: 2023,
};

let { title, type, year, company = "ubisoft", gamingTime: gT = 122 } = shit;

console.log(title);
console.log(type);
console.log(year);
console.log(company);
console.log(gT);

// Use already declared variables
({ title, year } = shit2);

console.log(title, year); // fifa 2023
```

	Javascript considers {a code block} therefore we'll get an error if we do not wrap {title, year} = shit2 inside (to show it's not a codeblock).
	
##### The rest pattern (...)

```javascript
let options = {
  title: "Menu",
  height: 200,
  width: 100
};

// title = property named title
// rest = object with the rest of properties
let {title, ...rest} = options;

// now title="Menu", rest={height: 200, width: 100}
alert(rest.height);  // 200
alert(rest.width);   // 100
```

##### Nested destructuring 

```javascript
const bigObject = {
  numbers: ["one", "two", "three"],
  measurments: {
    width: 20,
    height: 30,
  },
};

let {
  numbers: [i, j, k],
  measurments: { width, height },
  area = width * height,
} = bigObject;

console.log(i, j, k);
console.log(width, height);
console.log(area);
```

	Note that there are no variables for numbers and measurments, while area does not actually exist in bigObject object but it has a default value of 
	width * height.

#### The spread operator (...) 

The spread operator is expected to be used in places where it is accepted to use multiple values separated by a comma, usually it's either when we pass arguments in a function or when we want to create arrays.

	It doesn't create new variables ! 
	Instead, it takes elements from arrays and use them in places where we need values seperated by commas, well in fact it is similiar to destructuring because it helps us get elements from arrays.

```javascript
const array = [4, 5, 6];
const parray = [1, 2, 3];
const newarray = [1, 2, 3, ...array];

console.log(newarray); // [1,2,3,4,5,6]
console.log(...newarray); // 1 2 3 4 5 6 7 
```

	Iterbals are strings, arrays, sets and maps. NOT OBJECTS.

```javascript
// an example with function arguments

let randoms = [1, 2, 3];
const sum = function (a, b, c) {
  console.log(a + b + c);
};
sum(...randoms); // 6
```

##### The rest operator (...)

It does the opposite of **the rest operator** because it packs values into one array.

```javascript
const addition = function (...numbers) {
  let sum = 0;
  for (let n of numbers) sum += n;
  console.log(sum);
};

addition(1, 2); // 2
addition(1, 2, 3); // 6
addition(1, 2, 3, 4); // 10
```

##### Short circuiting (&& and ||)

For the `||` short circuiting after the first true value.
For the `&&` short circuiting after the first false value. 

#### The nullish coalescing  operator (??)

Introduced first in Es-2020, to solve many more problems because it behaves on nullish values and not false values.

	0 and '' are not nullish values, null or undefined are !

#### Logical assignment operators 

A more concise way to write `&& || ??` operators while assigning. 

	| |=    &&=   ??=

#### The for of loop 

A better way to loop over arrays.

```javascript
//we are here destructuing and then looping
// which makes it easier and more clean
for (const [i, el] of object.food.entries()) {
  console.log(`${i + 1}:${el}`);
}
```

##### Enhanced object literals 

```javascript
const random = {
  day1: "shit",
  day2: "shit-2",
  day3: "shit-3",
};

const object = {
  name: "mo",
  randoms,
  // a nice way to write methods vs function declarations
  log() {
    console.log(this.name);
  },
};

console.log(object);
```

![[Screenshot 2023-07-12 at 15.20.39.png]]

	Also note that we can compute certain values instead of validating them directly. 

##### Optional chaining (?.)

	If something?.proceed, if not something then it will return undefined.

```javascript
// If the method exists then it will be logged, if not then 
// "method not found !" will be logged.

console.log(object.shit?.() || "method not found !");

// On arrays 

const array =[];
console.log(array[0]?.name ?? "array empty !");

// array empty !
```

##### Looping objects 

Indirectly looping over objects using `keys (properties)` or `values` or `entries (keys along values stored in an array`.

```javascript
const time = {
  Monday: {
    open: "10 AM",
    close: "9 PM",
  },
  Thursday: {
    open: "10 AM",
    close: "9 PM",
  },
  Friday: {
    open: "10 AM",
    close: "9 PM",
  },
  Sunday: {
    open: "10 AM",
    close: "9 PM",
  },
};

const properties = Object.keys(time);
const values = Object.values(time);
const entries = Object.entries(time);

for (let [x, { open: o, close: w }] of entries)
  console.log(`${x}, we open at ${o} and close at ${w}.`);

// console.log(properties);
// console.log(values);
// console.log(entries);
```

![[Screenshot 2023-07-12 at 18.18.02.png]]

##### Sets 

	Sets and Maps are two new data structures added in ES6, before that, javascript only had objects and arrays as built-in data structures. 

The special thing and the the true addition of a `set` is that it does not allow duplicates ! 
W might enter many times the same value but that value will occur only once. 

	A set is a set of values without keys. (also iterable.)

Methods and properties for `Set` : 
- `new Set([iterable])` 
- `set.add(value)` - does nothing if the value exists, it just returns the set itself.
- `set.delete(value)` - removes the value, returns `true` if `value` existed at the moment of the call, otherwise `false`.
- `set.has(value)`– returns `true` if the value exists in the set, otherwise `false`.
- `set.clear()`
- `set.size`

The alternative to `Set` could be an array of users, and the code to check for duplicates on every insertion using `arr.find` but the performance would be much worse, because this method walks through the whole array checking every element. `Set` is much better optimized internally for uniqueness checks.

To iterate of `Sets` we have : 
- `set.keys()`
- `set.values()`
- `set.entries()` - returns an iterable of `[value,value]`, weird but actually exists for compatibility with `Map`. 

```javascript
let set = new Set(["uno", "dos", "whatever"]);

for (let x of set) console.log(x);

set.forEach((value, sameValue, set) => {
  console.log(value);
});
```

As we see in here `sameValue`  literally means the same value and we're passing `3 argumenst` just for the sake of compatibility with `Map`.

##### Maps 

A Map is a collection of keyed data items, just like an object. But a map accepts any type of keys `strings or bools or numbers etc`.

Methods and what they do : 
- `new Map()` - creates a map.
- `map.set(key,value)` - stores the value by the key.

		Maps can also use objects as keys.

**Looping over maps**

- `map.keys()` - returns an iterable of keys.
- `map.values()` - returns an iterable for values.
- `map.entries()` - returns for entries `[key,value]`.

```javascript
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);

// iterate over keys (vegetables)
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// iterate over values (amounts)
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// iterate over [key, value] entries
for (let entry of recipeMap) { // the same as of recipeMap.entries()
  alert(entry); // cucumber,500 (and so on)
}
```

	Map has also a built-in forEach method similiar to Array.

```javascript
// runs the function for each (key, value) pair
recipeMap.forEach( (value, key, map) => {
  alert(`${key}: ${value}`); // cucumber: 500 etc
});
```

We can create a Map from an object, by passing an iterable to a map `Object.entries` fits perfectly for this reason. 

```javascript
let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));
```

`Object.entries(obj)` return an array of `[key,value]` pairs. 
`[["name", "John"], ["age", 30]]`.

We can also create an object from a Map, using `Object.fromEntries()`.

```javascript
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map.entries()); // make a plain object (*)

// done!
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2
```


Here, `map.entries()` returns an iterable of  `[key, value]` pairs while also `map` is a pair of `[key,values]` iterable ! So we can use it in one line `let obj = Object.fromEntries(map)`

```javascript
let map = new Map();
map.set(1, "shit");
map.set(2, "fuck");
map.set(3, "hola");

const origi = {
  name: "mo",
  surname: "chaouki",
  age: 22,
};

for (let key of map.keys()) console.log(key);

let builtObj = Object.fromEntries(map);
let mapFromObject = new Map(Object.entries(origi));

console.log(builtObj);
console.log(mapFromObject);
```

#### Working with strings 
###### Working with strings - Part 1

**Used methods** :

- `string.length`
- `srting.indexOf`
- `string.lastIndexOf`
- `string.slice` : slice from `i` to `j-1`, `i and j-1` are included but `j` is not included !

		All string methods return primitives even if called on string objects.

### Working with strings [2]

### methods

string.toLowerCase() - string.toUpperCase() - string.trim() - string.replace()

`string.trim()` trim the string if it has any spaces !

`string.replace(/word/g,'by what to change')` /word/g means targetting every occurence of word and change it 'by what to change'

**methods that return booleans:**

string.includes() - string.startsWith() - string.endsWith()

### Working with strings [3]

### methods

.split() - .join() => split a string from a desired place, join it from a desired place.

.padStart() - .padEnd() => create some padding in a string with the {length,character} desired.

.repeat(n) => repeat a string n times.

----
# A closer look at functions 
### Default parameters 

In `ES-6` a new way of declaring default parameters has been introduced.
```javascript
function name (x=2,y=3,z=x*2){};
// note for the way z is written, that should always come at alst.
```

### Passing arguments by value vs by reference

	In javascript we only have passing by value, but when it comes to passing objects then we're really just passing the reference of that object in the memory heap as a value, which results in changing an object's properties if we're copying or mainting a property of that object inside a function. But  passing a primitive value and changing it inside a function won't change the actual value outside the function.

```javascript
const x = 2;
const oppo = {
  y: 2,
};

const hello = function (i, j) {
  i = 5;
  j.y = 5;
};

hello(x, oppo);
console.log(x, oppo.y); // x = 2 & oppo.y=5
```

### First class and higher order functions 

First class functions are just a concept or a feature that the language has, it means that javascript treats functions as values and they're just another type of objects. This means  that  also functions have methods. `function.bind() etc.`

- We can store functions in variables or properties.
- Pass functions as arguments to other functions.
- Return functions from functions.
- Call methods on functions. 

Higher order functions is indeed something we can see in practice, it means that a function can receive another function as an argument or a function that returns another functions, or both. 

- Function that receives  another function as an argument `x.addEventListener('click',doSomething);` 
- Function that returns a new function _(Somehow a very complicated concept to learn about.)_

### Functions accepting callback functions 

```javascript
const upperCase = function (string) {
  let [firstWord, ...otherWords] = string.split(" ");
  return [firstWord.toUpperCase(), ...otherWords].join(" ");
};

const transformer = function (string, fn) {
  console.log(fn(string));
};

transformer("mohammed chaouki is cs student.", upperCase);
```

What's so important about this is that It creates a logical abstraction, we hide details we do not need in another function that will only care about that specific details. In this case the `transformer` function doesn't care about how to make an uppercase string, all it cares about is to make that string uppercase with a hidden mechanism and then log it to the console. 

### Functions returning functions 

```javascript
const addons = function (x) {
  return function (y) {
    console.log(x + y);
  };
};

// call it this way
addons(2)(3);

// or this way
const n1 = addons(2);
n1(3);

// using arrow functions
const addonsArr = (x) => (y) => console.log(x + y);
addonsArr(2)(3);
```

### The call and apply method 

	We are going to set the this keyword manually, and why would we want that ? 

Everything is clear on this example : 

```javascript 
const bluePrint = {
  year: 2023,
  birthyear: 2001,
  calculateAge(name) {
    console.log(`${name} is ${this.year - this.birthyear}`);
  },
};

const mo = {
  year: 2023,
  birthyear: 2002,
};

const joe = {
  year: 2023,
  birthyear: 2001,
};

const calculateAge = bluePrint.calculateAge;

calculateAge.call(mo, "mo");
calculateAge.call(joe, "joe");

// we could also use apply
// apply expects an array of arguments

calculateAge.apply(mo, ["mo"]);
calculateAge.apply(joe, ["joe"]);

// but in modern javascript 
// we could simply use the call method 
```

### The bind method 

The bind method returns a function.

```javascript
const bluePrint = {
  year: 2023,
  birthyear: 2001,
  calculateAge(name) {
    console.log(`${name} is ${this.year - this.birthyear}`);
  },
};

const mo = {
  year: 2023,
  birthyear: 2002,
};

const joe = {
  year: 2023,
  birthyear: 2001,
};

const calculateAge = bluePrint.calculateAge;

const calcAgeMo = calculateAge.bind(mo);
const calcAgeJoe = calculateAge.bind(joe);

// fixing an argument
const hmida = calculateAge.bind(mo, "Hmida");

calcAgeMo("mohammed");
calcAgeJoe("joha");
hmida(); // Hmida is 21.
```

And we can actually set an argument to be fixed while binding ! 

	Partial application, part of the original function is already applied.

Bind with Event listeners solve a knot, we know that this keyword will point to the element we're calling the higher-function of `addEventListener` on, therefore we need to bind this keyword to the object owning that method we intend to use. 

```javascript
const button = document.querySelector('.buy');

const object {
	number : 0,
	add(){
	return this.number++;
	}
}

button.addEventListener('click',object.add.bind(object));
```

If we want to preset a value without caring about this keyword then we can do : 
`function.bind(null,argumentToPreset)`. Note that the order of arguments is important.

### Immediately invoked function expressions 

	Needed in async/await. 

`IIFE` means the function is executed only once and immediately, but the downfall of it is it creates it's own scope that  cannot be accessed globally (from the global scope). If we want this we would just wrap code inside a `block {code goes here}`. But still `IIFE` got so many use cases. 

```javascript
(function(){
	 console.log("thi will run only once !")
})();
```

### Closures 

	A function has access to the variable environment (VE) of the execution context in which it was created. 

In a case of closure, `JavaScript`  will firstly look in the closure for a variable before even looking at the scope chain.

> A closure is the closed-over __variable-environment __  of the execution context in which a function was created, even after that execution context is gone.

```javascript
const increment = function () {
  let i = 0;
  return function () {
    i++;
    console.log(i);
  };
};

const plusplus = increment();

plusplus(); // 1
plusplus(); // 2
plusplus(); // 3
```

>  A closure has priority over the scope chain

---

# How the DOM really works 

> DOM is a very complex API that contains lots of methods and properties to intercat with the DOM tree.

> There are different types of nodes in the DOM, some are html elements and some are just texts. 

![[Screenshot 2023-07-15 at 00.08.53.png]]

As we see in the screenshot, we have a lot of node types ! They all benefit from a mechanism called inheritance which makes this organization work, every child type inherits from it's ancestor methods and properties until we get to the `EventTarget` type node type.

`Node` and `Window` inherits some properties from `EventTarget` like `addEventListener` etc.

```javascript
// Selecting elements
document.documentElement;
document.head;
document.body;

document.querySelector('.header');
document.querySelectorAll('.section'); // Returns a nodeList 

document.getElementById('section--1');

// Both of these return an htmlCollection
document.getElementByTagName('button');
document.getElementsByClassName('btn');

// Creating and Inserting elements 
document.createElement('div');
message.classList.add('className');
message.textContent = 'some text ...';
message.innerHTML = 'some text <button>fuck</button>';

header.prepend(message); // make it as first child
header.append(message); // make it as last child

// To make more copies of the element
header.append(message.cloneNode(true));

header.before(message); // make it as a sibling before
header.after(message); // make it as a sibling after

// Delete elements
message.remove();

```

> An html collection is a live collection of html elements that updates live if any change occurred, either an element is deleted or added etc.

```javascript
// Styles 
message.style.backgroundColor = '#171717';
message.style.width = '100px';

getComputedStyle(message).color;
getComputedStyle(message).height;

document.documentElement.style.setProperty('--color-primary','blue');

// Attributes
logo.alt;
logo.className;

logo.alt = "hola";

// Non-standard (will be revield ad undefined)
logo.designer;
// Non-standar (but we can get it)
logo.getAttribute('designer');

logo.setAttribute('company','mego');

logo.src; // will get the asbolute link
logo.getAttribute('src'); // will get the relative link
// same goes for href

// Data attributes 
// it starts with data 
logo.dataset.nameOfData;

// Classes
logo.classList.add('');
logo.classList.remove('');
logo.classList.toggle('');
logo.classList.contains('');

// Don't use 
logo.className = 'name'; // it will overrides every other class
```

Sometimes we might wanna remove an event after it was triggered only once, therefore we need `element.removeEventListener`.

### Event propagation : Bubbling and capturing

The event is generated in the root document then the capturing phase begins where the event travels down to the element that triggered the event, there begins the target phase and the event bubbles up to the root document again passing by parent elements only and no sibling, this is important because we can listen to the even in one of the parent elements.

> Not all events are generated in the document root, some event are generated in the target.

```javascript
e.target; // where the event was triggered
e.currrentTarget; // the target which is attached to the event handler
e.currentTarget === this; // they both refer to the element attached to the event handler

e.stopPropagation(); // as it says, stop bubbling.
```

> Events are captured while traversing from the document root to the target, event handlers are not picking up these events during the capture phase, instead, event listeners listen to event during the bubbling phase, that is the default  behaviour of `addEventListener` method. The reason for that is that capturing phase is irrelevant for us, the bubbling phase can be more useful for event delegation.

To catch events during the capturing phase, we can do this : 

```javascript
element.addEvenListener('click', function(){}, true);
// while seeting the 3rd parameter to true, the event handler will no longer listen to bubbling events instead it will listen to capturing events.
```

### Event delegation 

> Event delegation is far better than attaching event handlers for multiple elements.

	See example of implementing smooth scrolling.

### DOM traversing

It means selecting an element based on another elements.

```javascript
// Going downward
element.childNodes; // has everything inside (text,comments,etc.)
element.children; // html collection
element.firstElementChild;
element.lastElementChild;

// Going upwards : parents
element.parentNode;
element.parentElement;
element.closest(query string goes here); // for direct parent 

// Sideways
element.previousElementSibling;
element.nextElementSibling;
// nodeList
element.previousSibling;
element.nextSibling;
```

### Passing arguments to event handlers

> A handler function can only accept one real argument.

```html
<nav>
  <ul class="navlinks">
    <li class="link"><a class="item">Home</a></li>
    <li class="link"><a class="item">Contact</a></li>
    <li class="link"><a class="item">Share</a></li>
  </ul>
</nav>
```

```javascript
const nav = document.querySelector("nav");
const link = document.querySelector(".link");
const ul = document.querySelector("ul");

const bigevent = function (e) {
  if (e.target.classList.contains("item")) {
    const over = e.target;
    const siblings = link.closest(".navlinks").querySelectorAll(".item");
    siblings.forEach((el) => {
      if (el !== over) el.style.opacity = this;
    });
  }
};

nav.addEventListener("mouseover", bigevent.bind(0.5));
nav.addEventListener("mouseout", bigevent.bind(1));
```

----
## OOP 
### Constructor function

```javascript 
const Identity = function (fullName, nationality, age) {
  // Instance propreties
  this.fullName = fullName;
  this.nationality = nationality;
  this.age = age;
  // 	never use this:
  // 	this.calcAge = function name(params) {
  //  		console.log(2030-this.age)
  // 	}
};

const user1 = new Identity("Mohammed Chaouki", "Moroccan", 21);
const user2 = new Identity("Manal Marouan", "Moroccan", 45);
console.log(user1);
console.log(user2);

console.log(user1 instanceof Identity); // true
console.log(user2 instanceof Identity); // true
```

> About the never use this, for a purpose of having a lot of instances we should never write a method that way because it's a bad practice and kills performance. We should use prototypes.

- An empty object `{}` is created.
- The function is called, and in this function call the `this` keyword will be set to this newly created object.
- `{}` is linked to a prototype.
- Function automatically return `{}`.

> Note that all of this happens because of the `new` keyword !

> `user1, user2` are instances of `Identity`.

### Prototypes 

Each function has a property called `prototype`.

```javascript
Identity.prototype.calcAge = function() {
	console.log(2023 - this.age);
}
```

> `Identity.prototype` is a property of the constructor function and not the prototype of `Identity`, Instead it means the prototype of linked objects that were created using the constructor function.

> `__proto__` is actually the prototype of the created objects. eg. `user1.__proto__`. 
> This property is created once the object is created and linked to it's prototype. 

```javascript
Identity.prototype.isPrototypeOf(user1); // true
Identity.prototype.isPorotypeOf(Identity); // false
// define an instance using Prototypes
Identity.prototype.state = "OK";
// own propreties and not
user1.hasOwnProprety(fullName); // true
user1.hasOwnProprety(state); // false
```

An own property is a property defined using the constructor, while not an own property is the one define using the prototype.

Objects inherit methods from their prototype, which is very convenient  
because we only have to define methods once and then use them for  
many objects !

This is know by the prototype chain, every prototype has a prototype since  
a prototype is an object too, more deeply this means that objects are  
linked through prototypes and the prototype of the prototype is  
`Object.prototype` which it's prototype is `null` .

```javascript
user1.hasOwnProprety(fullName);
// hasOwnProprety is not a method defined in the constructor function
// but it is actually inherited from the prototype of the prototype
// user1.__proto.__proto
```

![[Screenshot 2023-07-18 at 00.57.53.png]]


> `console.dir()` shows a directory of a function.

```javascript
// class declaration
class Identity {
  constructor(fullName, age) {
    this.fullName = fullName;
    this.age = age;
  }
  // methods will be added to .prototype proprety (like before)
  calcAge() {
    console.log(2040 - this.age);
  }
}

const mohammed = new Identity("Mohammed chaouki", 22);
// the following line is true
mohammed.__proto__ === Identity.prototype;
// and of course the prototype of mohammed (mohammed.__proto__)
// is the prototype of objects created by that class (constructor)
// which is Identity.prototype
```

 
Things to keep in mind:

- Classes are not hoisted even we use class declaration.
- Classes are first citizens (we can pass them into functions and return them from functions).
- Classes are executed in strict-mode (body of classes).

> Use classes or constructors, matter of preference !

### Getters and setters

```javascript
class Person {
  constructor(firstName, fullName, age) {
    this.firstName = firstName;
    this.fullName = fullName;
    this.age = age;
  }
  // methods will be added to .prototype proprety (like before)
  calcAge() {
    console.log(2040 - this.age);
  }
  // set existing propreties (use the _ as a convention)
  set firstName(name) {
    this._firstName = name.split(" ")[0];
  }
  get firstName() {
    return this._firstName;
  }
}
const perso1 = new Person("Mohammed", "Mohammed chaouki", 20);
console.log(perso1);
```

> Read more aboout setters and getters !

### Static methods
Let's start by this example : 
```javascript
Array.from(); // it will work

[1,2,3].from(); // it won't work 
```

`from()` method is attached to the `Array` constructor and it's not present in the prototype, so it won't be inherited.

```javascript
// function constructor
Identity.staticmethod = function () {
  console.log("hello");
};
Identity.staticmethod();
// this keyword refers to the constructor

// class
class Hola {
	Constructor (x,y,z) {
		this.x=x;
		this.y=y;
		this.z=z;
	}
	// Instance methods
	calcAge () {
		console.log(2090 - this.x);
	}
	// Static method
	static staticmethod() {
	 console.log("hello");
	}	
}

Hola.staticmethod();
// this keyword refers to the constructor 
```

### Inheritance between "classes" : constructor functions

> The call() allows for a function/method belonging to one object to be assigned and called for a different object.
> > 
>  call() provides a new value of this to the function/method. With call(), you can write a method once and then inherit it in another object, without having to rewrite the method for the new object.

```javascript
const Parent = function (firstName, birthyear) {
  this.firstName = firstName;
  this.birthyear = birthyear;
};

Parent.prototype.calcAge = function () {
  console.log(2022 - this.birthyear);
};

const parent1 = new Parent("Mo", 2001);

const Child = function (firstName, birthyear, status) {
  Parent.call(this, firstName, birthyear);
  this.status = status;
};

// Linking prototypes
// this should happen here before creating any other methods for the Child class, because this line will create an empty object which will result in overwriting any other methods if it happens after ..

Child.prototype = Object.create(Parent.prototype);

Child.prototype.maritalS = function () {
  console.log(`I am ${this.status}`);
};

const child1 = new Child("Simo", 2001, "single");

child1.maritalS();
child1.calcAge();

// Linking prototypes causes :
console.log(child1 instanceof Parent);
// this is obvious
console.log(child1 instanceof Child);
// fixing the constructor problem pointing to Parent
Child.prototype.constructor = Child;

console.dir(Child.prototype.constructor);
```

> Check handwritten notes again !

### Inheritance between classes : ES6 classes

```javascript
class Person {
  constructor(firstName, fullName, age) {
    this.firstName = firstName;
    this.fullName = fullName;
    this.age = age;
  }
  // methods will be added to .prototype proprety (like before)
  calcAge() {
    console.log(2040 - this.age);
  }
  // set existing propreties (use the _ as a convention)
  // beacause we're setting an already existing proprety
  set firstName(name) {
    this._firstName = name.split(" ")[0];
  }
  get firstName() {
    return this._firstName;
  }
}
const perso1 = new Person("Mohammed", "Mohammed chaouki", 20);

class Citizen extends Person {
  // if we do need new propreties then do this
  constructor(firstName, fullName, age, major) {
    // always at first
    super(firstName, fullName, age, major);
  }
}
```

### Inheritance between classes : object.create

```javascript
const Big = {
  init(firstName, birthYear) {
    this.firstName = firstName;
    this.birthYear = birthYear;
  },
  calcAge() {
    console.log(2022 - this.birthYear);
  },
};

const Small = Object.create(Big);
console.log(Small.__proto__ === Big); // true

Small.init = function (firstName, birthYear, major) {
  Big.init.call(this, firstName, birthYear);
  this.major = major;
};

const small1 = Object.create(Small);
small1.init("Mohammed", 2001, "computer science");
small1.calcAge();
```

> Rewatch `Another class example !` video later on !

### Protection, Encapsulation, Privacy 

`_proprety` a convention to protect a property.

```javascript
class Shit {
  // public field
  locale = navigator.language;
  // private field
  #birthYear;

  constructor(firstName, birthYear) {
    this.firstName = firstName;
    this.#birthYear = birthYear;
  }

  // private method
  #calcAge() {
    const age = console.log(2022 - this.#birthYear);
    return this;
  }

  revealAge() {
    return this.#calcAge();
  }

  revealBirthYear() {
    console.log(this.#birthYear);
  }
}

const trial1 = new Shit("Mohammed", 2001);
trial1.revealAge().revealBirthYear();
```

> To make chaining possible, we must return the object as the last thing in the method this way, we make sure that after calling a method we want to chain, the object is returned as if we are calling the next method on the object !

> Watch classes summary after a week `29 july 2023` to refresh my memory.

# Asynchronous javascript

### Synchronous code 

Everything i have been writing till now is synchronous code which means, 
- Code is executed line by line.
- Each line of code waits for the previous one to be executed.
- Long running operations block code execution.

### Asynchronous code

```javascript
const p = document.querySelector('.p');
setTimeout(function () {
	p.textContent = 'Hola';
}, 5000);
p.style.color=red;
```

The callback function will run after the time is finished, code will be executed without waiting for the callback to finish therefore the callback will be executed as the last one.

`setTimeout` is asynchronous.

- Asynchronous code is executed after a task that runs in the background finishes.
- Asynchronous code is non-blocking.
- Execution does not wait for an asynchronous task to finish it's work.
- Callback functions alone do not make code asynchronous.
- Callbacks do not automatically make code asynchronous, it's just `setTimeout` has an async behaviour. 

> `image.src` is loading an image asynchronously, after the image is loaded a `load` event will be omitted and the we can listen to this event and attach a callback function to it.

- `addEventListener` does not make automatically code async, and can't make async on it's own too !

### AJAX

>  AJAX, Asynchronous Javascript And XML. 

It allows us to communicate with remote web servers in an asynchronous way, with AJAX calls we can request data from web servers dynamically. 

- Request (GET, POST, etc.)
- Response.

> API, Application Programming Interface which is a piece of software that can be used by another piece of software in order to allow applications to communicate to each other. 
> > There are many APIs in we dev such as,
> > - DOM API.
> > - Geolocation API.
> > - Own Class API.
> > - Online API (application running on a server that receives requests for data and sends data back as a response).
> 
> XML is a data format that is not used anymore, JSON is instead used. 
>

```javascript
const request = new XMLHttpRequest();
request.open('GET','url');
request.send();
// Then we wait asynchronously for a load event
request.addEventListener('load', function() {
	// JSON format is only text so we need to transform it to an object
	const [data] = JSON.parse(this.responseText);
	console.log(data);
})
```

### Callback hell

It simply means a callback inside a callback function and it keeps going uglier if we need to send an AJAX call depending on the previous AJAX call.

### Promises and the FETCH API

> How to escape callback hell.

A promise in an object that is used as a placeholder for the future result of an async operation. 

- We no longer need to rely on events and callbacks passed into asynchronous functions to handle asynchronous results.
- Instead of nesting callbacks, we can chain promises for a sequence of asynchronous operations, escaping callback hell.


> [!NOTE] A callback
> Check JS canvas for an illustration explaining 

> For now we only use fetch api to build promises.
> > We consume a promise when we have a promise, after it is built.

### Consuming promises

```javascript
const request = fetch("https://restcountries.com/v3.1/name/morocco")
  .then((response) => response.json())
  .then(([data]) => console.log(data));

console.log(request);
```

- The fetch api returns a promise.
- The `response.json()` also returns a promise.
- Finally we consume the value as intended `data`.

### Chaining promises
All clear !

```javascript
const request = fetch("https://restcountries.com/v3.1/name/morocco")
  .then((response) => response.json())
  .then(([data]) => {
    console.log(data.name.common);
    const neighbour = data.borders?.[0] ?? "No borders !";
    return fetch(`https://restcountries.com/v3.1/name/${neighbour}`);
  })
  .then((response) => response.json())
  .then(([data]) => console.log(data.name.common));

console.log(request);
```

### Handling rejected promises

We can either handle them by passing another callback function into the second parameter for the `then` method.

Or, we catch them globally at the end using `catch` method.

```javascript
const request = fetch("https://restcountries.com/v3.1/name/morocco")
  .then((response) => response.json())
  .then(([data]) => {
    console.log(data.name.common);
    const neighbour = data.borders?.[0] ?? "No borders !";
    return fetch(`https://restcountries.com/v3.1/name/${neighbour}`);
  })
  .then((response) => response.json())
  .then(([data]) => console.log(data.name.common))
  .catch((err) => {
    console.error(`${err} :( !`);
  })
  .finally(() => console.log("happend anyways !"));
```

- `then()` happens if the promise is fulfilled.
- `.catch()` happens if the promise is rejected, and it also returns a promise.
- `.finally()` happens in both cases.

### Throwing errors manually

```javascript
const getJSON = function (url, errorMsg = "Something is wrong !") {
  return fetch(url).then((response) => {
    if (!response.ok) throw new Error(errorMsg);
    return response.json();
  });
};

const request = getJSON(
  "https://restcountries.com/v3.1/name/japan",
  "Country not found :( !"
)
  .then(([data]) => {
    console.log(data.name.common);
    const neighbour = data.borders?.[0];
    if (!neighbour) throw new Error("neighbour not found");
    // const neighbour = "ddddd";
    //
    return getJSON(
      `https://restcountries.com/v3.1/name/${neighbour}`,
      "Country not found !"
    );
  })
  .then(([data]) => console.log(data.name.common))
  .catch((err) => {
    console.error(`${err} :( !`);
  });

console.log(request);
```

### Asynchronous behind the scenes


> [!NOTE] To do
> Read hand written notes about the event loop.

### Building a simple promise

```javascript
const lotteryPromise = new Promise(function (resolve, reject) {
  console.log("Lottery draw is happening !");
  setTimeout(function () {
    if (Math.random() >= 0.5) resolve("You win !");
    else reject("You lose !");
  }, 2000);
});

lotteryPromise
  .then((response) => console.log(response))
  .catch((err) => console.error(err));

// Promisifying

const wait = function (seconds) {
  return new Promise(function (resolve) {
    setTimeout(resolve, seconds * 1000);
  });
};

wait(1)
  .then(() => {
    console.log("1 sec passed");
    return wait(2);
  })
  .then(() => {
    console.log("2 sec passed");
    return wait(3);
  })
  .then(() => {
    console.log("3 sec passed");
  });

Promise.resolve("Resolved immidiately !").then((x) => console.log(x));
Promise.reject("Rejected immidiately !").catch((x) => console.error(x));
```

> Promisifying is converting callback based async behaviour to promise based.
> > Wrapping `code` inside a promise that will be returned from a function that is wrapping all the logic.

### Consuming promises with async/await

```javascript
const getData = async function () {
  try {
    const response = await fetch(url, options);
    const data = await response.json();
    console.log(data);
    renderData(data);
    renderTopAnimes(data);
    scopeRenderer(data);
  } catch (err) {
    console.error(err);
  }
};

getData();
```

The `await` stops execution of function code until we get a promise fulfilled returned.

> Error handling using `try...catch` is understandable as i already remember it.

### Returning values from async functions


> [!NOTE] TO DO
> Rewatch video again !

### Running promises in parallel

`Promise.all()` is a promise combinator.  Used to process multiple parallel promises that  don't depend on one another.

> If one promise is rejected then it short circuits the mechanism and all other promises will be rejected.


> [!NOTE] To do
> Read documentation about other promise combinators, `Promise.race - Promise.allSettled - Promise.any `
> 


# Modern javascript 

### Modules in javascript 


> [!NOTE] To do
> Read theory about modules

### ES6 modules in practice

Imports are a live connection of exports and not copies.

### Top level await

> Be careful with it since it can block code to execute, use it when needed carefully !


> [!NOTE] How modules are executed
> The importing module executes code from the exporting module, blocking code .. then completing executing normally. 
> 

### The module pattern

### CommonJs modules 







