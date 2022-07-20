## What is special about a generator function 


```js title="Normal function"
function normalFunction() {
  console.log("Hello");
  console.log("World");
}
```

* Run to complemetion model.
* Output: 'Hello' 'World'
* Exit by returning or throwing an error.
* If you call the function again, it will begin the execution from the top.

```js title="Generator function"
function* generatorFunction() {
  yield `Hello`;
  yield `World`;
}
```

!!! warning

    Do not forget the * after function key : `function* generatorFunction()`

* A generator is a function that can stop midway and then continue from where it
stopped.

* A generator function can "pause" the execution.
* To achieve that behaviour, we use the `yield` keyword.
* `yield` is an operator with which a generator can pause itself.
* Generator yields a value.

## Invocation

Generators

```js title="Create the Generator"
function* generatorFunction() {
  yield `Hello`;
  yield `World`;
}

const generatorObject = generatorFunction();
```

```js title="Use the Generator"
for(const word of generatorObject) {
  console.log(word);
}
// Log: Hello world

console.log([...generatorObject]);
// Log: [ 'Hello', 'world' ]

generatorObject.next();
// Returns { value: ‘Hello’, done: false }

generatorObject.next();
// Returns { value: ‘World', done: false }

generatorObject.next();
// Returns { value: undefined, done: true }

```