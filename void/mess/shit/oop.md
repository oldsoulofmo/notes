### Object oriented programming

#### Function constructors

A constructor is a way of creating objects programmatically and assigning a prototype  
to the objects we create.

> A constructor enables you to provide any custom initialization that must be done before any other methods can be called on an instantiated object.

Which means that we create the blueprint of an object and then we define instances  
and methods to this object. To give life to this object  
we use `new constructorFunctionName ()` .

> As a convention function constructors starts with a Majuscule.

```javascript
const Identity = function (fullName, nationality, age) {
  // Instance propreties
  this.fullName = fullName;
  this.nationality = nationality;
  this.age = age;
  // 	never use this:
  // 	const calcAge = function name(params) {
  //  		console.log(2030-this.age)
  // 	}
};

const user1 = new Identity("Mohammed Chaouki", "Moroccan", 21);
const user2 = new Identity("Manal Marouan", "Moroccan", 45);
console.log(user1);
console.log(user2);
```

#### Prototypes

`Identity.prototype` is actually the prototype of linked objects  
and not the prototype of Identity !  
`object.__proto__` is simply the prototype of jonas.

```javascript
Identity.prototype.isPrototypeOf(user1); // true
// define an instance using Prototypes
Identity.prototype.state = "OK";
// own propreties and not
user1.hasOwnProprety(fullName); // true
user1.hasOwnProprety(state); // false
```

> An own proprety is a proprety defined using the constructor,  
> not an own proprety is the one define using the prototype.

#### Prototypal inheritance

Objects inherit methods from their prototype, which is very convenient  
beacause we only have to define methods once and then use them for  
many objects !

This is know by the prototype chain, every prototype has a prototype since  
a prototype is an object too, more deeply this means that objects are  
linked through prototypes and the prototype of the prototype is  
`Object.prototype` which it's prototype is `null` .

```javascript
user1.hasOwnProprety(fullName);
// hasOwnProprety is not a method defined in the constructor function
// but it is actually inherited from the prototype of the prototype
// user1.__proto.__proto
```

`console.dir() // shows a directory of a function ...`

#### Es6 classes

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
- Classes are first citizens (we can pass them into functions and return them from functions)
- Classes are executed in strict-mode (body of classes)

> Use classes or constructors, matter of preference !

#### Getters and Setters

:warning: Read more about how to use setters and getters !

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

#### Static methods

```javascript
// function constructor
Identity.staticmethod = function () {
  console.log("hello");
};
Identity.staticmethod();
// this keyword refers to the constructor
// class
static staticmethod() {
 console.log("hello");
}
Person.staticmethod();
// this keyword refers to the entire class
```

#### Object.create

We define the prototype by itself then attach it to objects by creating new objects linked through prototypes ( As the code bellow shows ) .

```javascript
// create the prototype which will be linked to the created objects
const Prototype = {
  // initialize the instances

  init(firstName, lastName, age) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
  },

  calcAge() {
    console.log(2040 - this.age);
  },
};

const user1 = Object.create(Prototype);

user1.init("Mohammed", "Chaouki", "22");
user1.calcAge();

// true
user1.__proto__ = Prototype;
```

#### Inheritance Between "Classes": constructor functions

> The call() allows for a function/method belonging to one object to be assigned and called for a different object.
>
> > call() provides a new value of this to the function/method. With call(), you can write a method once and then inherit it in another object, without having to rewrite the method for the new object.

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

:warning: Check hand written notes !

#### Inheritance Between "Classes": ES6 Classes

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

#### Inheritance Between "Classes": Object.create

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

Small.init = function (firstName, birthYear, major) {
  Big.init.call(this, firstName, birthYear);
  this.major = major;
};

const small1 = Object.create(Small);
small1.init("Mohammed", 2001, "computer science");
small1.calcAge();
```

#### Encapsulation & chaining methods

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

> to make chaining possible, we must return the object as the last thing in the method this way, we make sure that after calling a method we want to chain, the object is returned as if we are calling the next method on the object !
