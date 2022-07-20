
# Iterables & Iterators

## Intro

### Iterable Protocol - Technical details

* The iterable protocol decides whether an object is an iterable or not.
* An object is iterable when it contains a method at the key `[Symbol.iterator]` that takes no arguments and returns an object which conforms to the iterator protocol.

### Iterator Protocol - Technical details

* The iterator protocol decides whether an object is an iterator.
* An object is an iterator when it satisfies the following rule
* The object must have a next() method that returns an object with two properties
  1. value: which gives the current element
  2. done: which is a boolean value indicating whether or not there are any more elements that could be iterated upon

* Each time you call the next() method, it returns the next value in the collection.
* `{ value: 'next value', done: false }` // till the last element has been returned
* `{ value: undefined, done: true}` // after the last element has been returned

## For..of loop

* A `for..of` loop with a **string** will iterate over the characters in the string

```js
for(const char of str) {
  console.log(char);
}
```

* A `for..of` loop with a **map** will iterate over the key/value pairs of the map:

```js
for (const [key, value] of map) {
  console.log(key + ' = ' + value);
}
```

* A `for..of` loop with an **array** will iterate over the items in the array:

```js
for(const item of arr) {
  console.log(item);
}
```

* A `for..of` loop with a **set** will iterate over the values in the set:

```js
for (const value of set){
  console. log(value);
}
```

## Iterables & Iterators examples

### Basic example

```js title="Create the iterator"
const range = {
  [Symbol.iterator]: () => {
    let counter = 1;
    const iterator = {
      next: () => {
        const result = { value: counter, done: false };
        if (counter <= 50) {
          counter++;
          return result;
        }
        return { done: true };
      }
    }
    return iterator;
  }
}
```
```js title="Use iterator"

for (const num of range) {
  console.log(num);
}
// output: 1 2 3 ... 50

console.log([...range]);
// output: [ 1, 2, 3, ...50 ]
```

* Our range iterable logs numbers from 1 to 50 when we have the default iteration with the `for..of` loop.
* Customize the iteration behaviour.
* Pass three values namely start, end and interval.
* Print the range starting from start value till the end value with interval size increments.
* start=10, end=20 and interval = 2 logs10, 12, 14, 16, 18 and 20 in the console.

### Example with `next()` and `return()`

```js title="The iterator object"

const customRange = {
  [Symbol.iterator]: (start = 1, end = 50, interval = 1) => {
    let counter = start;
    const iterator = {
      next: () => {
        const result = { value: counter, done: false };
        if (counter <= end) {
          counter += interval;
          return result;
        }
        return { done: true };
      }
    }
    return iterator;
  }
}

```

```js title="Use the iterator object"
for (const num of customRange) {
  if ( num > 10 ) {
    break;
  }
  console. log(num);
}
// Output : 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
```

!!! info

    Note that the return method is invoked when the iteration is stopped prematurely


```js title="Iterator object use with for"
for (const num of customRange) {
  console.log(num);
}
// Output : 1, 2, 3, 4, 5, 6, 7, 8, 9, ... 50

console.log([ ...customRange ]);
// Output : [1, 2, 3, 4, 5, 6, 7, 8, 9, ... 50 ]
```

```js title="Iterator object use with while"
const iterator2 = customRange[Symbol.iterator](10, 20, 2);

let result = iterator2.next();
while(!result.done) {
  console.log(result.value);
  result = iterator2.next();
}
// output: 10 12 14 16 18 20  
```

```js title="Iterator object use with next"
const iterator = customRange[Symbol.iterator](10, 20, 2);

iterator.next();
// output : { value: 10, done: false }
iterator.next();
// output : { value: 12, done: false }
iterator.next();
// output : { value: 14, done: false }
iterator.next();
// output : { value: 16, done: false }
iterator.next();
// output : { value: 18, done: false }
iterator.next();
// output : { value: 20, done: false }
```