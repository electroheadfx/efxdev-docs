# Timeouts & Intervals

## setinterval()

* The `setinterval()` function repeatedly runs the same code over and over again at regular intervals.

```js
setInterval(function, duration, param1, param2, ...);
```

* The first parameter is the code to execute.

* *The second parameter is the duration in milliseconds.

* After the second parameter, you can pass in zero or more values that represent any parameters you want to pass to the function when it is run.

```js
function greet() {
  console.log("Hello");
}

setInterval(greet, 20090)
// -> Logs ‘Hello’ every 2 seconds
```

## clearInterval()

* Intervals keep running a task forever so you should clear the interval when appropriate.

```js
const intervalId = setInterval(greet, 2000, 'Vishwas');
clearInterval(intervalId);
```

## setInterval & setTimeOut: Noteworthy points

* It is possible to achieve the same effect as setinterval with a recursive setTimeout.

```js
setTimeout(function run() {
  console.log('Hello')
  setTimeout(run, 100);
}, 100);
// output 'Hello' to endless loop each 100ms
```

1. Duration is guaranteed between executions:

  * Irrespective of how long the code takes to run, the interval will remain the same.
  * Code can take longer to run the the time interval itself? Recursive `setTimeout`.

2. You can calculate a different delay before running each iteration.

```js
setInterval( () => {
  console.log( ‘Hello’ )
}, 100);

```

1. The duration interval includes the time taken to execute the code you want to run:

* The code takes 40ms to run, the interval is 60ms
* The code takes 50ms to run, the interval is 50ms

2. setinterval is always a fixed interval duration