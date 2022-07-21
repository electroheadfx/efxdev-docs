## Set intro

The Set object in JavaScript lets you store unique values of any type.

```js
const set = new Set();
```

To append values to the Set object, use the add method passsing in the value as its argument.

```js
const set = new Set();

set.add(1);
set.add(2);
set.add(1); //  -> Does not get added
```

To check the number of values in the set, you can use the size property.

```js
const set = new Set();

set.add(1);
set.add(2);

set.size; // -> Returns 2
```

To check if a value exists in the set, use the `has` method.

```js
set.has(1); // -> Returns true
set.has(5); // -> Returns false
```

To remove a value from the set, use the `delete` method passing in the value. To delete all the
values in the set, use the `clear` method.

```js
set.delete(1); // -> Returns true
set.delete(5); // -> Returns false

set.clear();
set.size; // -> Returns 0
```

## Set and Array Conversion

```js title="Array to Set"
const numArr = [1, 2];
const numSet = new Set([numArr]);
```

```js title="Set to Array"
const numArr = [1, 2];
const numSet = new Set(numArr);

// just deconstruct set
[...numSet]
```

## Iterating over a Set

```js
const set = new Set();
set.add(1);
set.add(2);

for (let value of set) {
  console.log(value);
}
// output: 1 2
```