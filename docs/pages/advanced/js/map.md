# Map object

## Intro

The Map object in JavaScript holds key-value pairs (similar to an object).

```js
const map = new Map();
```

To add key value pairs use the set method passing in key and value as its arguments.

```js
const map = new Map();

map.set('firstName','Bruce');
map.set('lastName', 'Wayne');
```

To check the number of key value pairs in the map, use the size property.

```js
const map = new Map();

map.set('firstName', 'Bruce');
map.set('lastName', 'Wayne');

map.size;
// -> Returns 2
```

To get the value at a particular key, use the get method passing in key as the argument.

```js
map.get('firstName');
// -> Returns 'Bruce';

map.get('lastName');
//  -> Returns 'Wayne';
```

To check if a key exists in the map, use the has method.

```js
map.has('firstName');
// -> Returns true

map.has('fullName');
//-> Returns false
```

To remove a key value pair from the map, use the delete method passing in the key."To delete all the key value pairs in the map, use the clear method

```js
map.delete('firstName');
// -> Returns true

map.delete(‘fullName');
// -> Returns false

map.clear();
map.size;
// -> Returns 2
```

## Map array conversion

```js title="2D array to map"
const personArr = [ ['firstName', 'Bruce'], ['lastName', 'Wayne'] ];
const personMap = new Map(personArr);
```

```js title="Map to array"
const map = new Map()

map.set('firstName', 'Bruce');
map.set('lastName', 'Wayne');

const arr = Array.from(map);
```
## for in Map

```js title="Iterating over a Map"
const map = new Map();

map.set('firstName', 'Bruce');
map.set('lastName', 'Wayne');
```

```js title="Iterate over key-value pairs"
for (let [key, value] of map) {
  console.log(key + ' = ‘ + value);
}
```

```js title="Iterate over keys only"
for (let key of map.keys()) {
  console.log(key);
}
```

```js title="Iterate over values only"
for (let value of map.values()) {
  console.log(value);
}
```

## Map VS object

### 1. key type

!!! info

    * A Map's keys can be any value (including functions, objects, or any primitive).
    * The keys of an Object however must be either a String or a Symbol.

```js
const keyString = 'a string';
const keyObj = {};
const keyFunc = function() {};

myMap.set(keyString, 'String key value');
myMap.set(keyObj, 'Object key value');
myMap.set(keyFunc, 'Function key value');
```

### 2. Accidental keys

* A Map does not contain any keys by default.
* An Object however has a prototype, so it contains default keys.

### 3. Identifying the size

* Number of items in a Map is easily retrieved from its 'size' property.
* The number of items in an Object however, must be determined manually.

### 4. Iteration behaviour

* Map is an iterable so it can directly be iterated

* Iterating over an Object however requires obtaining its keys in some fashion and then iterating over them.