# Les bases de TS

## 1-Les types de base

```ts
let str = "str"
let num = 5
let array = []
let obj = {
    a: 5
}
let toggle = true

let anything;
let randomNumber : number;

const conversion = (celsius : number) => {
    return (celsius * 9/5) + 32;
}

console.log(conversion(50));
version(50));
```

## 2- Les Tableaux  et les Objets

> **Les tableaux**

```ts
const fruits = ['fraise', 'pomme']
fruits.push("cerises")
console.log(fruits);

const mixedArray = [1, 'txt', [1,2,3]]

let nums : number [];
nums.push(1) // erreur
nums = [1,2,3]

let nums2 : number [] = []
nums2.push(2)

let random : any []; 
random = [true, false, true]
```

> **Les Objets**

```ts
const car = {
    name: "Audi",
    model: "A1",
    km: 70000
}

car.name = 4 // erreur

let profile : {
    name: string, 
    age: number,
    hobbies: string[]
}

profile = {
    name: "John",
    age: 85,
    hobbies: []
}

let user : {
    name: string,
    age: number,
    favFood: string[],
    data: any
} = {
    name: "Joe",
    age: 45,
    favFood: ['pasta', 'cheese'],
    data: 50
}

let obj: object;

obj = {name: "Enzo"}
```

## 3- Les Fonctions

```ts
function multiply(num1 : number, num2 = 10, action?: string)   {
    if(action) console.log(action);
    return num1 * num2;
}
console.log(multiply(6,10,"create"));

let foo: Function;

foo = () => {}
```

> **Function signatures**

```ts
let baz: (a: number, b:number) => number;

baz = (a,b) => a + b;


// Callback
function greetings(fn: (a: string) => void) {
    fn("Hello World")
}

function printToConsole(msg: string) {
    console.log(msg);
}

greetings(printToConsole)
```

## 4- Les Unions et les custom types

> **Les Unions**

```ts
let code : string | number | boolean | object | Function;
code = 5

let arr : (boolean|number)[]
arr = [true, false, 999]

const foo = (param: number|string) => {
    console.log(param);
}
foo('Test')
```

> **Les Types Perso**

```ts
type mixedNumStr = number | string;
type booleanOrObject = boolean | object;

const baz = (param: mixedNumStr | booleanOrObject) => {
    console.log(param);
}
baz(true)

type element = {
    x: number;
    y: number;
    id: number | string;
    visible: boolean;
}

const button : element = {
    x: 99,
    y: 50,
    id: 999,
    visible: true
}
```

## 5- Tuple et Enum

> Tuple

```ts
let tuple : [boolean, number]
tuple = [false, 20]
```

> **Enum**

```ts
const Roles = {
    JAVASCRIPT: 1,
    CSS: 2,
    REACT: 3
}
console.log(Roles.JAVASCRIPT);

enum Roles {JAVASCRIPT = 1, CSS, REACT}

console.log(Roles);
```

## 6- Interfaces

```ts
interface Rocket {
    reactors: number;
    vMax: number;
    takeOff: (action: string) => void
}

interface Rocket {
    price: number;
    carburant: number;
}
```

```ts
class RocketFactory implements Rocket {
    reactors: number;
    vMax: number;
    price: number;
    carburant: number;

    constructor(
            reactors: number, 
            vMax: number,
            price: number,
            carburant: number) {
        this.reactors = reactors;
        this.vMax = vMax;
        this.price = price;
        this.carburant = carburant;
    }
    takeOff(action: string){
        console.log(action);
    }
}
const Falcon1 = new RocketFactory(12,900,2,9000)
console.log(Falcon1);
Falcon1.takeOff('Décollage')
```

## 7- Le DOM

> **Type Assertion**

```ts
let txt:string;
txt = "str"
```

> **Assertion**

```ts
const form : HTMLFormElement = document.querySelector('form')!
console.log(form.children);
```

> **Type Casting**

```ts
const form = document.querySelector('form') as HTMLFormElement
console.log(form.children);
const input = document.querySelector('input') as HTMLInputElement


form.addEventListener('submit', handleSubmit)

function handleSubmit(event : Event){
    event.preventDefault()
    console.log("SUBMITTED");
}

window.addEventListener('click', handleClick)

function handleClick(event: MouseEvent) {
    console.log(event.clientX, event.clientY);
}

const paragraphsList = document.querySelectorAll('p');
```
