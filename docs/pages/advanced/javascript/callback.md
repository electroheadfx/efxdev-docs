## Intro

!!! info

    In JavaScript, functions are first class objects :

    * Just like an object, a function can be passed as an argument to a function
    * A function can also be returned as values from other functions

```js title="A simple function callback"
function greet(name) {
  console.log(`Hello ${name}`);
}

function greetVishwas(greetFn) {
  const name = "Vishwas";
  greetFn(name);
}

greetVishwas(greet);

// output: 'Hello Vishwas'
```

```js title="A higherOrder Function callback"
function greet(name) {
  console.log(`Hello ${name}`)
}

function higherOrderFunction(callback) {
  const name = "Vishwas"
	callback(name)
}

higherOrderFunction(greet);

// output: 'Hello Vishwas'
```

* Any function that is passed as an argument to another function is called a **callback function** in JavaScript
* The function which accepts a function as an argument or returns a function is called a **higher order function**

## Synchronous callbacks

!!! info

    A callback which is executed immediately is called a synchronous callback.

```js title="A synchronous callback test"
function greet(name) {
  console.log(`Hello ${name}`);
}

function higherOrderFunction(callback) {
  const name = "Vishwas";
  callback(name);
}

higherOrderFunction(greet);

// output: 'Hello Vishwas'
```

```js title="A synchronous callback with js built-in function"
let numbers = [1, 2, 4, 7, 3, 5, 6];

numbers.sort((a, b) => a - b);
// output: [ 1, 2, 3, 4, 5, 6, 7 ]

numbers.map(n => n*2);
// output: [ 2, 4, 6, 8, 10, 12, 14 ]

numbers.filter(n => n % 2 === 0);
// output: [ 2, 4, 6 ]
```

## Asynchronous callbacks

```js title="Asynchronous Example with a setTimeout"
function greet(name) {
  console.log(`Hello ${name}`);
}

setTimeout(greet, 2000, 'Vishwas');

function callback() {
  document.getElementById("demo").innerHTML = "Hello World";
}

// output: 'Hello Vishwas' after a delay of 2 secs
```

```js title="Asynchronous Example with addEventListener"
document.getElementById("btn").addEventListener("click", callback);
```

```js title="Asynchronous Example with a get"
$.get( "url", function( data ) {
  $(".result").html( data );
  alert( "Load was performed." );
})
```

* Callback functions allow you to delay the execution of a function.