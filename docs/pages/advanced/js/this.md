## `this` with Arrow fonction

!!! question

    **What is logged to the console in this code?**

```js title="Lexical binding"
const person = {
  firstName: 'Vishwas',
  lastName: 'Batman',
  sayMyName() {
    const fullName = () => {
      return `${this.firstName} ${this.lastName}`;
    }
    console.log(`Full name is ${fullName()}`);
  }
}
person.sayMyName();

```

!!! answer

    Line 8: 'Full name is Vishwas Batman'

* Unlike normal functions, an arrow function does not define a `this` keyword at all.
* `this` keyword in an arrow function behaves like any other variable.
* It is going to lexically resolve to an enclosing scope that does define this keyword.

## `this` without Arrow fonction

!!! question

    **What is logged to the console in this code?**

```js
const person = {
  firstName: 'Vishwas',
  lastName: 'Batman',
  sayMyName() {
    const fullName = function() {
      return `${this.firstName} ${this.lastName}`;
    }
    console.log(`Full name is ${fullName()}`);
  }
}
person.sayMyName();
```

!!! answer

    Line 8: 'Full name is undefined undefined'

* Problem is that implicit binding is on the `sayMyName` function
* Within sayMyName, `this` points to the person object
* On line 8, `fullName()` has no implicit, explicit or new binding
* Defaults to global binding
* Within the `fullName` function, this points to the window object
* In the global scope, we don't have any variables called `firstName` or `lastName`

## `this` with `new` Binding

* We can invoke a function with the 'new' keyword.
* In such a scenario, the function is invoked with this referencing an empty object.

```js
function Person(name) { 
  // constructor function
  this.name = name;
}

const pl = new Person('Vishwas');
const p2 = new Person('Batman');
```

* When we invoke a function with the new keyword, JavaScript under the hood will create a new empty object that 'this' keyword will reference to.

* Add properties to that object using this followed by the dot notation.

* When a function is invoked with the new keyword, within that function this keyword will always reference a new empty object.

## `this` Implicit Binding

```js
const person = {
  name: 'Vishwas',
  sayMyName() {
    console.log(`My name is ${this.name}`);
  }
};

person.sayMyName();
// -> 'My name is Vishwas'
```

* When a function is invoked with the dot notation, the object to the left of that dot is what the this keyword is referencing.
* `this` keyword is referencing the `person` object.

## `this` with Object : implicit Binding

Fallback if none of the other three rules are matched.

```js
function sayMyName () {
  console.log(`My name is ${this.name}`);
}

sayMyName() // My name is undefined
```

```js
var name = 'Vishwas';
function sayMyName () {
  console.log(`My name is ${this.name}`);
}

sayMyName(); // My name is Vishwas
```

!!! important

    If none of the three rules are satisfied, JavaScript will default to the global scope and set `this` keyword to the window object.

## `this` with `bind`

```js title="Explicit Binding"
const person = {
  name: 'Vishwas'
}

function sayMyName () {
  console.log(`My name is ${this.name}`);
}
// -> 'My name is '
```

Bind works similar to the call method but instead of invoking the function, it returns a new function that you
can invoke whenever you wish to.

```js title="Bind method"
const person = {
  name: 'Vishwas'
}

function sayMyName (hobby1, hobby2) {
  console.log(`My name is ${this.name}`, `I'm interested in ${hobby1} and ${hobby2}`);
}

const sayMyNameVishwas = sayMyName.bind(person, 'Chess', 'Football');

sayMyNameVishwas();
// -> My name is Vishwas. I'm interested in Chess and Football
```

## `this` with `call`

Every function has a built in method named `call` which allows you to specify the context with which a function is
invoked.

```js title="call method"
const person = {
  name: 'Vishwas'
}

function sayMyName () {
  console.log(`My name is ${this.name}`);
}

sayMyName.call(person);
// -> 'My name is Vishwas'
```

* The first argument passed to call is what `this` keyword inside sayMyName is referencing.
* If you want to specify arguments to your function, you can pass them in after the first argument to call.


```js
const person = {
  name: 'Vishwas'
}

function sayMyName (hobby1, hobby2) {
  console.log(`My name is ${this.name}`, `I'm interested in ${hobby1} and ${hobby2}`);
}

sayMyName.call(person, 'Chess', 'Football');
// -> My name is Vishwas. I'm interested in Chess and Football
```

## `this` with `apply`

Every function has a built in method named `apply` which allows you to specify the context with which a function is invoked.

```js title="apply method"
const person = {
  name: 'Vishwas'
}

function sayMyName () {
  console.log(`My name is ${this.name}`);
}

sayMyName.apply(person);
// -> 'My name is Vishwas'
```

* The first argument passed to apply is what `this` keyword inside sayMyName is referencing.
* apply expects an array as its second argument.

```js
const person = {
  name: 'Vishwas'
}

function sayMyName (hobby1, hobby2) {
  console.log(`My name is ${this.name}`, `I'm interested in ${hobby1} and ${hobby2}`);
}

sayMyName.apply(person, ['Chess', 'Football']);
// -> My name is Vishwas. I'm interested in Chess and Football
```

## `this` `apply` vs `call`

* call takes in a comma separated arguments.
* apply takes in array as arguments.

**c**all : **c**omma
**a**pply : **a**rray

!!! important

    `call` and `apply` which invoke a function right away with the context you have specified.
