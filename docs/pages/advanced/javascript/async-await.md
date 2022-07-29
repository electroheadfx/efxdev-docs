## Intro

!!! info

    - The async keyword is used to declare async functions
    - Async functions are functions that are instances of the AsyncFunction constructor
    - Unlike normal functions, async functions always return a promise

```js title="Normal function"
function greet() {
  return "Hello";
}
greet();
// browser console: "Hello"
```

```js title="async function"
async function greet() {
  return "Hello";
}
greet();
// browser console: Promise {<fulfilled>: "Hello"}
```

```js title="async function with promise"
async function greet() {
  return Promise.resolve("Hello");
}

greet().then(
  value => console.log(value)
);
// browser console: ‘Hello’
```

## Await

!!! info

    **Await** keyword can be put infront of any async promise based function to pause your code until that promise settles and returns its result await only works inside async functions. Cannot use await in normal functions

```js title="async with await"
async function greet() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("Hello"), 1000)
  });

  let result = await promise; // await until the promise resolve

  console.log(result) ; // "Hello"
}

greet()
```

## Sequential execution

```js title="Function hello"
function resolveHello() {
  return new Promise(resolve => {
    setTimeout(() => resolve( ‘Hello’ ), 2000);
  }
};
```

```js title="Function world"
function resolveWorld() {
  return new Promise(resolve => {
    setTimeout(() => resolve( ‘Hello’ ), 2000);
  }
};
```

```js title="Sequential start"
async function sequentialStart() {
  const hello = await resolveHello();
  console.log(hello); // Logs me after 2 secondes

  const world = await resolveWorld();
  console.log(world); // Logs after 2 + 1 = 3 seconds
}
sequentialStart();
```

## Parrallel execution

```js title="resolveHello fn"
function resolveHello() {
  return new Promise(resolve => { 
    setTimeout(() => {
      resolve('Hello');
    }, 2000);
  });
}
```

```js title="resolveWorld fn"
function resolveWorld() {
  return new Promise(resolve => {
    setTimeout(function () {
      resolve('World');
    }, 1000)
  });
}
```

```js title="parallel function"
function parallel() {
  Promise.all([
    (async () => console.log(await resolveHello()))(), // Total time taken = 2 seconds
    (async () => console.log(await resolveWorld()))(), // Total time taken = 1 seconds
  ]);
}
parallel();

// Logs 'World' in first then: 'Hello'
// Total time taken : 2 secs
```

```js title="parallel function with await"
async function parallel() {
  await Promise.all([
    (async () => console.log(await resolveHello()))(), // Total time taken = 2 seconds
    (async () => console.log(await resolveWorld()))(), // Total time taken = 1 seconds
  ]);
  console.log('Finally'); // Logged after World Hello
}

parallel();
// Logs 'World' in first then: 'Hello' 'Finally'
```

## Chaining promises vs async-await

```js title="with 'then'"
const promise = fetchCurrentUser( api/user’ )
promise
  .then(result => fetchFollowersByUserId(° api/followers/${result.userId} ))
  .then(result => fetchFollowerInterests( api/interests/${result.followerId} ))
  .then(result => fetchInterestTags( api/tags/${result.interestId} ))
  .then(result => fetchTagDescription( api/description/${result.tagId} ))
  .then(result => console.log('Display the data', result));
```

```js title="with 'await'"
async function fetchData() {
  const user = await fetchCurrentUser('api/user');
  const followers = await fetchFollowersByUserId(`api/followers/${result.userId}`);
  const interests = await fetchFollowerInterests(`api/interests/${result.followerId}`)
  const tags = await fetchInterestTags(`api/tags/${result.interestId}`);
  const description = await fetchTagDescription(`api/description/${result.tagId}`);
  console.log('Display the data', result);
}
```

```js title="with 'await' and 'try..catch'"
async function fetchData() {
  try {
    const user = await fetchCurrentUser('api/user');
    const followers = await fetchFollowersByUserId(`api/followers/${result.userId}`);
    const interests = await fetchFollowerInterests(`api/interests/${result.followerId}`)
    const tags = await fetchInterestTags(`api/tags/${result.interestId}`);
    const description = await fetchTagDescription(`api/description/${result.tagId}`);
    console.log('Display the data', result);
  } catch(e) {
    console.log('Error', e);
  }
```

## Exercise - async await

!!! question

    **Problem statement:**

    * Define a function called sleep which accepts a duration parameter
    * The sleep function should suspend execution of the function it is invoked in

```js title="Solution"
function sleep(duration) {
  return new Promise(resolve => setTimeout(resolve, duration));
}

async function main() {
  console.log('Logs immediately');
  await sleep(2000);
  console.log('Logs after 2 seconds');
}

main();

// output: 'Logs immediately'
// then output: 'Logs after 2 seconds'
```