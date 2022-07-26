## Filter

!!! info

    The **filter()** method take an arg function with array element like parameter. The function return a `boolean`filter. An second parameter may be used for element indice. Filter return an array.

```js title="Simple Example"
const users = ['John', 'Marc', 'Mattew', 'Peter', 'Paul'];
const result = users.filter(user => user.length > 4);
// return name length > 4
// result return: Array["Mattew", "Peter"]

const result = users.filter((user, i) => i > 2);
// return indice > 2
// result return: Array["Peter", "Paul"]
```

### Filter example with an object

```js title="Intial data"
const users = {
  "admin": false,
  "user": true,
  "super": true
}
```
#### Output all true data from user object

```js title="Solution"
Object.keys(users).filter(
  (k) => {
    return user[k]
  }
);
// Output: [ 'user', 'super' ]
```

```js title="shortland solution"
Object.keys(users).filter(
  (k) => user[k]
);
// Output: [ 'user', 'super' ]
```

## Map

!!! info

    **map** take an arg function with array element like parameter.
    The function must return the new value. An second parameter may be used for element indice. Map return an array.

```js title="Simple Example"
const users = ['John', 'Marc', 'Mattew', 'Peter', 'Paul'];
const result = users.filter(user => user.length > 4);
// result return: Array["Mattew", "Peter"]

const result = users.filter((user, i) => i > 2);
```

## Reduce

!!! info

    The **reduce()** method executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

```js title="Simple Example"
const array1 = [1, 2, 3, 4];
const reducer = array1.reduce((acc, element) => acc + element);
// return 10

const reducer2 = array1.reduce((acc, element, i) => acc + element + i);
// return 16
```

### Reduce Exemple

```js title="Intial data"
const pilots = [
  {
    id:10,
    name: "Peo Dameron",
    years: 30,
  },
  {
    id:2,
    name: "Temin Wexley",
    years: 50,
  },
  {
    id:41,
    name: "Tallissan Lintra",
    years: 13,
  },
  {
    id:99,
    name: "Ello Asty",
    years: 5,
  },
];

```

```js title="Get the lower age pilot"
const pilot = pilots.reduce(
    (acc, element) => (acc.years || 0) < element.years ? acc : element
);

// Output : { id: 99, name: 'Ello Asty', years: 5}
```

[More reduce practices](reduce-cases.md){ .md-button .md-button--outline }
