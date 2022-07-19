# # ES Module

```js
//fichier /helper/math/simple-math.js
export function somme(a, b) {
  return a + b
}
export let auteur = 'Euler'
export const PI = 3.14

// the default export
export default function multiplication(a, b) {
  return a * b
}
```

```js
// import the default
import math from 'helper/math/simple-math'
// or any name you need
import myMath from 'helper/math/simple-math'
// or import default and the others modules in one line:
import math, {auteur, PI, somme} from 'helper/math/simple-math'
// you can change module name normal export (author)
import math, {auteur as author, PI, somme} from 'helper/math/simple-math'

math(6, 6) // retourne 36
somme(6, 6) // retourne 12
console.log(author) // return Euler
console.log(PI) // return 3.14
```

# Template literal

```jsx
let a = 5
let b = 10
const name = 'toto'
console.log(`Mon nom ${name} & Quinze vaut ${a + b} etnon ${2 * a + b}.`)
// "Quinze vaut 15 et
// non 20."
```

# Destructuring

> With **Object**

```js
const personne = {nom: 'john', prenom: 'doe', age: 25, ville: 'paris'}

function sayHello(personne) {
  const nom = personne.nom
  const prenom = personne.prenom
  const age = personne.age
  const ville = personne.ville
  console.log(`Bonjour ${nom} ${prenom} tu as ${age} à ${ville}`)
}
// ↓ identique à ↓

//même fonction mais avec la destructuration
function sayHello(personne) {
  const {nom, prenom, age, ville} = personne
  console.log(`Bonjour ${nom} ${prenom} tu as ${age} à ${ville}`)
}

//on peut aussi faire la destructuration en parametre
function sayHello({nom, prenom, age, ville}) {
  console.log(`Bonjour ${nom} ${prenom} tu as ${age} à ${ville}`)
}
```

> With **Array**

```js
const toto = ['un', 'deux', 'trois']

// sans utiliser la décomposition
const un = toto[0]
const deux = toto[1]
const trois = toto[2]
// en utilisant la décomposition
const [un, deux, trois] = toto
```

> With **function**

```js
const personne = {nom: 'john', prenom: 'doe', age: 25, ville: 'paris'}
const showPersonne = ({nom, prenom, age, ville}) => {
    console.log(`Bonjour ${nom} ${prenom} tu as ${age} à ${ville}`)
}
showPersonne(personne)
```

# Shortlang

```js
const prenom = 'codeur'
const age = 'bali'
const ville = 'paris'
// instead to do this:
const personne = {prenom: prenom, age: age, ville: ville}
// do:
const personne = {prenom, age, ville}
```

# Arrow function

[Fonctions fléchées - JavaScript | MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Functions/Arrow_functions)]

```js
//fonctions classiques
function sayHello() {
  return 'hello'
}
function sayHelloName(name) {
  return 'hello ' + name
}
function somme(a, b) {
  return a + b
}
//fonctions fléchées
const sayHello = () => 'hello'
const sayHelloName = name => 'hello ' + name
const somme = (a, b) => a + b

const somme = (a, b) => {
  let c = a + b
  return c
}
```

# Nullish coalishing

It allow to avoid js error with null or undefined data.

[Nullish coalescing operator Docs](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

```jsx
function sayHello(name) {
  let nameSafe = name ?? 'anonyme'
  return `Bonjour ${nameSafe}`
}

sayHello() // Bonjour anonyme
sayHello(null) // Bonjour anonyme
sayHello('Mike') // Bonjour mike
```

# Optional chaining

[Optional chaining Docs](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

For using data in object we need to test them if it's not *undefined*:

```js
const countryCode = personne.adress.country.code
//❌ non null safe
//Uncaught TypeError: Cannot read property 'country' of undefined

// manage the null safe
if (personne && personne.adress && personne.adress.country) {
  const countryCode = personne.adress.country.code
}
// or
const countryCode = personne && personne.adress && personne.adress.country.code
```

With ES6 we can use the optional chaining :

```js
const countryCode = personne?.adress?.country?.code
// return the data or null without error
```

# Ternal operator

[L'opérateur conditionnel Doc](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

```js
//méthode classique
function welcome(isAdmin) {
  if (isAdmin) {
    return 'Hello Admin'
  } else {
    return 'Hello Member'
  }
}
//équivalent en ternaire
function welcome(isAdmin) {
  return isAdmin ? 'Hello Admin' : 'Hello Member'
}
```

# Array methods in ES6

[Array.prototype.every() - Docs](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/every)

```js
const computers = [
  {
    id: 'pc-1',
    name: 'MacBook Pro',
    features: [
      'usb-c',
      'screen-15',
      'batterie',
      'keyboard',
      'webcam',
      'ssd-1to',
    ],
  },
  {
    id: 'pc-2',
    name: 'Lenovo',
    features: ['usb-a', 'screen-15', 'batterie', 'keyboard', 'ssd-500go'],
  },
  {
    id: 'pc-3',
    name: 'MSI',
    features: [
      'usb-a',
      'screen-13',
      'batterie',
      'keyboard',
      'webcam',
      'ssd-500go',
    ],
  },
]
```

Use with :

> `map` => `array`

```js
computers.map(computer => 'Brand/'+computer.name)
// ['Brand/MacBook Pro', 'Brand/Lenovo', 'Brand/MSI']
```

> `forEach`` => executes your code once for each array element

```js
computers.forEach(computer => { console.log(computer.name) } )
// 'MacBook Pro'
// 'Lenovo'
// 'MSI'

let computerListName = [];
computers.forEach(function(item){
  computerListName.push(item);
});
// computerListName = [ 'MacBook Pro', 'Lenovo', 'MSI' ]
```

> `filter` (with `includes`) => `array`

```js
// output only computers with 'screen-15' feature
computers.filter(computer => computer.features.includes('screen-15'))
// [{id: 'pc-1', ..etc}, {id: 'pc-2', ...}]
```

> `some` => `boolean`

```js
// test if there is any computer with ''ssd-2to' feature
computers.some(computer => computer.features.includes('ssd-2to'))
// output false
```

> `every` => `boolean`

```js
// Test if every computer has feature like 'ssd-1to' or 'keyboard'
computers.every(computer => computer.features.includes('ssd-1to'))
// output false
computers.every(computer => computer.features.includes('keyboard'))
// output true
```

> `find` => first `element` that satisfies the provided testing function

```js
// Find every computer which are ''MacBook Pro' (it found one)
computers.find(computer => computer.name === 'MacBook Pro')
// {id: 'pc-1', name: 'MacBook Pro', ...}
```

> `reduce` => `value` from the calculation on the preceding element

*The scheme is : `array.reduce((accumulator, element)`*

```js
// Output every computer's features in any array with a spray operators
computers.reduce((allFeatures, computer) => {
 return [...allFeatures, ...computer.features]
}, [])
// output :
// [ 'usb-c', 'screen-15', 'batterie', 'keyboard', 'webcam', 'ssd-1to',
//   'usb-a', 'screen-15', 'batterie', 'keyboard', 'ssd-500go', 'usb-a',
//   'screen-13', 'batterie', 'keyboard', 'webcam', 'ssd-500go' ]
```

#### Exemple with filter and map

Find every computer with `webcam` and output their names.

```js
const webCamPcName = computers
    .filter( computer => computer.features.includes('webcam') )
    .map( computer => computer.name );

console.log(webCamPcName);
// [show MacBook Pro, MSI]
```

# Rest parameters

```jsx
Math.min(100, 10, 1) // retoune 1

const arr = [5, 6, 8, 4, 9]
Math.min(arr[0], arr[1], arr[2], arr[3], arr[4])

// Same thing with with Rest
Math.min(...arr)
```

# Spread operator

```js
// spread with object
const personne = {nom: 'mike', prenom: 'codeur', adresse: 'bali'}
const personne2 = {...personne, rue: 17}

// spread with array
let numberStore = [0, 1, 2];
let newNumber = 12;
numberStore = [...numberStore, newNumber];
```

# Promise Async Await

[Promise - JavaScript | MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Promise)

> Voir le cours plus évolué dans advanced `async-await` et `callback`

- Create the promise :

```js
//création d'un promise
function simulationFetch(duration = 0) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (duration > 400) {
        reject(`KO Timeout`)
      } else {
        resolve(`OK`)
      }
    }, duration)
  })
}
```

- Use the promise

```js
simulationFetch(100).then(callBackOK, callBakcError)

simulationFetch(100).then(
  e => console.log(e),
  err => console.error(err),
) // OK
simulationFetch(500).then(
  e => console.log(e),
  err => console.error(err),
) // KO
```

- Use the promise with async/await

```js
async function simulationFetchAsyncSuccess() {
  const result = await simulationFetch(200)
  return `success: ${result}`
}

async function simulationFetchAsyncFailed() {
  const result = await simulationFetch(500)
  return `failed: ${result}` // ne devrait pas etre executé
}

async function simulationFetchAsyncCatch() {
  let result
  try {
    result = await simulationFetch(500, true)
    return `failed: ${result}` // this would not be executed
  } catch (error) {
    return `failed and recovered: ${error}`
  }
}
```
