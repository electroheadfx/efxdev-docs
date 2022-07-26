## Initial data

```js
let list = [4, 5, 6];
```

## 'for in' iterate on keys

```js
for (let i in list) {
   console.log(i);
   // Output: 0, 1, 2,

   console.log(list[i]);
   // Output: 4, 5, 6
}
```

## 'for of' iterate on values

```js
for (let i of list) {
   console.log(i);
   // output: "4", "5", "6"
}
```

## 'forEach' iterate on values with a callback

```js
list.forEach( (id) => {
  console.log(id);
  // Output: "4", "5", "6"
})
```

## Bonus with promise

### Promise with for..of
> Ouput the user ID with 1000 ms delay one per one

```js
// Create the promise with timeout
const getUserID = (id) => {
  return new Promise( (resolve) => {
		setTimeout(() => {
      console.log(`Got user ID ${id}`);
      resolve(id);
	  },1000);
  })
}
```

```js
( async function() {
	const users = [30,20,10,5,1];
  for (const user of users) {
  	await getUserID(user)
  }
})()

// output at 1000 ms frequence one per one the users (5 x 1000 ms):

// 'Got user ID 30' >1000 ms
// 'Got user ID 20' >1000 ms
// 'Got user ID 10' >1000 ms
// 'Got user ID 5'  >1000 ms
// 'Got user ID 1'  >1000 ms
```

### Promise with forEach, map or for

```js
// with forEach, map, for, it run in parrallels
users.forEach( async(user) => {
  await getUserID(user)
})
// output with 1000 ms delay All the users in one time:
```