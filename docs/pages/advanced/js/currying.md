```js title="Currying and closures"

function curry (fn) {
  return function (a) {
    return function (b) {
      return function (c) {
        return fn(a, b, c);
      }
    }
  }
}

const sum = (value1, value2, value3) => value1 + value2 + value3;

const curriedSum = curry(sum);
console.log(curriedSum(2)(3)(5));

// output: 10
```

* Currying is possible because of closures.

* When we return a function from another function, we are returning the function along with its lexical scope.

* Lexical scope takes the outer function parameters into consideration.