## Calculate price basket

```js title="Initial object"
const caddie = [
  { book: 1, price: 19.99 },
  { beer: 6, price: 4.5 },
  { bread: 1, price: 1.2 }
];
```

```js title="Calculate the caddie price"
const price = caddie.reduce((acc, curr) => acc + curr.price, 0);
console.log(price.toFixed(2)); // 25.69
```

## Reformat data in object

```js title="Initial object"
const musicians = [
  {
    id: 12345,
    firstName: "Stevie",
    lastName: "Tay Vaughn",
    instrument: "Guitar"
  },
  {
    id: 8877,
    firstName: "Jaco",
    lastName: "Pastorius Vaughn",
    instrument: "Bass Guitar"
  },
  { id: 87, firstName: "Mitch", lastName: "Micthele", instrument: "Drums" }
];
```
!!! tip

    Its Easier to call the date by the ID in a object (instead of search) :

```js title="Get musicians list"
const musiciansList = musicians.reduce((acc, curr) => {
  const { id, ...othersProps } = curr;
  acc[id] = othersProps;
  return acc;
}, {});
console.log(musiciansList); // return { 87:{...}, 8877:{...}, 12345:{...} }
console.log(musiciansList[87]); // return Micth object
```

## Calculate the number of pizzas

```js title="Initial object"
const pizzas = [
  { userName: "Bob", pizzaName: "Marguarita", qty: 1 },
  { userName: "Sam", pizzaName: "Veggie", qty: 2 },
  { userName: "John", pizzaName: "Regina", qty: 3 },
  { userName: "Kim", pizzaName: "Regina", qty: 1 },
  { userName: "James", pizzaName: "Calzone", qty: 1 },
  { userName: "Morley", pizzaName: "Marguarita", qty: 5 }
];
```
!!! tip

    Give the number of pizza per type :

```js
const pizzaPerType = pizzas.reduce((acc, curr) => {
  if (Object.keys(acc).includes(curr.pizzaName)) {
    acc[curr.pizzaName] += curr.qty;
  } else {
    acc[curr.pizzaName] = curr.qty;
  }
  return acc;
}, {});

console.log(pizzaPerType);
// Output : { Marguarita: 6, Veggie: 2, Regina: 4, Calzone: 1 }
```
