## Intro

* The setTimeout() function executes a particular block of code once after a specified time has elapsed.

```js
setTimeout(function, duration, param1, param2, ...);
```

* The first parameter is a function to run, or a reference to a function defined elsewhere.

* The second parameter is a number representing the duration in milliseconds to wait before executing the code.

* After the second parameter, you can pass in zero or more values that represent any parameters you want to pass to the function when it is run.

```js
function greet() {
  console.log('Hello');
}

setTimeout(greet, 2000);
// -> Logs 'Hello’ to the console after 2 seconds
```

```js
function greet(name) {
  console.log('Hello ${name}');
}

setTimeout(greet, 2000, 'Vishwas');
// -> Logs 'Hello Vishwas' to the console after 2 seconds
```

## Clear a timeout

* To clear a timeout, you can use the clearTimeout() method passing in the identifier returned by setTimeout as a parameter.

```js
function greet() {
  console.log('Hello');
}

const timeoutId = setTimeout(greet, 2000, 'Vishwas');
clearTimeout(timeoutId);
// -> Nothing is logged to the console
```

* Amore practical scenario is clearing timeouts when the component is unmounting to free up the resources and also prevent code from incorrectly executing on an unmounted component.