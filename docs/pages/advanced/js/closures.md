## Double incovation

```js title="Double Invokation" linenums="1"
function outer() {
  let counter	= 0;
  function inner() {
    counter++;
    console.log(counter);
	}
	inner();
}

outer();
outer();

// What is logged to the console?
// Line 5 : 1
// Line 6 : 1
```

* Every time a function gets invoked, it gets a brand new local memory which contains all the variables and arguments.

* When we finish running the function, that temporary memory is pretty much deleted.

* When we invoke the function again it doesn't remember the data that was stored in the memory from the previous run.

## Invoke later


```js title="Invoke later" linenums="1"
function outer() {
  let counter =	0;
  function inner() {
    counter++;
    console.log(counter);
  }
  return inner;
}

const fn = outer();
fn();
fn();

// What is logged to the console?
// Line 5 : 1
// Line 6 : 2
```

* Closures in JavaScript

* A closure is the combination of a function bundled together with references to its surrounding state (the lexical environment).

* Closures are created every time a function is created, at function creation time.

* In JavaScript, when we return a function from another function, we are effectively returning a combination of the function definition along with the function's scope chain.

* This would let the function definition have an associated persistent memory which could hold on to live data between executions.

!!! info

    The combination of the function and its scope chain (lexical environemnt) is what is called a closure in JavaScript.

## Multiple closure instances

```js title=""
function outer() {
  let counter = 9
  function inner() {
    counter++
    console. log(counter)
  }
  return inner
}

const fn1 = outer();
fn1();
fn1();

const fn2 = outer();
fn2();
fn2();

// What is logged to the console?
// fn1 output: 10 11
// fn2 output: 10 11
```

!!! info

    Multiple closure instances don't share the same persistent memory.

## Exercice: memoization with Closures

### Implement optimizedSquare function

```js title="First implementation"
function square (num) {
  return num * num;
}

function memoizedSquare () {
  let cache = {};
  return function optimizedSquare (num) {
    ...
  }
}
```

```js title="Final implementation"
function square (num) {
  return num * num;
}

function memoizedSquare () {
  let cache = {};

  return function optimizedSquare (num) {
    if (num in cache) {
      console.log('Returning from cache');
      return cache[num];
    } else {
      console.log('Computing square');
      const result = square(num);
      cache[num] = result;
      return result;
    }
  }
}
```

### Testing the optimizedSquare memo closure

```js title="Run memoizedSquare"
const memoSquare = memoizedSquare();

console.log(memoSquare(2));
console.log(memoSquare(5));
console.log(memoSquare(5));

// What is logged to the console?
// Computing square 4
// Computing square 25
// Returning from cache 25
```

### Generic memoization implementation

```js title="memoize function"
function memoize(callback) {
  let cache = {};

  return function(...args) {
    const key = args.toString();
    if (key in cache) {
      console.log("Returning from cache");
      return cache[key];
    } else {
      console.log("Computing result");
      const result = callback(...args);
      cache[key] = result;
      return result;
    }
  }
}
```

```js title="Use the memoize fn with a callback"
// the callback
function add(a, b) {
  return a + b;
}

// Create the memo with the callback
const memoizedAdd = memoize(add);
console.log(memoizedAdd(2,4));
console.log(memoizedAdd(2,4));

// What is logged to the console?
// Computing result 6
// Returning from cache 6

```