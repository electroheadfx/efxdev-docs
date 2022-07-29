# TypeScript Avancé

### Type et Interface

> **Intersection**

```ts
type Fish = {
    fin: number;
    element: "water";
    gills: true;
}
type Shark = {
    weight: number;
    length: number;
}
type HammerheadShark = Fish & Shark & {
    test: "abc"
};

const shark1: HammerheadShark = {
    fin: 3,
    element: "water",
    gills: true,
    weight: 500,
    length: 200,
    test: "abc"
}

let obj: {
    prop1: "a"
} & {
    prop2: "b"
}
```

> **Lier des interfaces**

```ts
interface Flower {
    pollen: true;
    type: "vegetal"
}
interface Rose extends Flower {
    color: string;
    thorn: boolean;
}
const RedRose: Rose = {
    pollen: true,
    type: "vegetal",
    color: "Rose",
    thorn: true
}
```

> **Union discriminante**

```ts
type Japan = {
    lang: "JA";
    food: string[];
}
type Italy = {
    lang: "IT";
    food: string[];
}
type Country = Japan | Italy;

const automaticResponse = (country: Country) => {
    if(country.lang === "JA") {
        console.log("Hello Japan");
    } else if (country.lang === "IT") {
        console.log("Hello Italy");
    }
}
const Japanese1 : Country = {
    lang: "JA",
    food: ["Ramen", "Sushis"]
}
automaticResponse(Japanese1)
```

> **Unknown number of props**

```ts
interface Group {
    [name: string] : object;
}
const spainTrip: Group = {
    john: {id: 1},
    tom: {id: 2},
    julia: {id: 3},
}
```

## 2- Opérateurs

> **L'opérateur : !**

```ts
const container = document.querySelector(".container")!;
// console.log(container.children);
```

> **L'opérateur : ?**

```ts
type Job = {
    title: string;
    description?: string;
    salary: number;
}
const user1: Job = {
    title: "Dev Front-End",
    description: "Développeur de sites internet.",
    salary: 30000
}
// console.log(user1?.description);
```

> **Optional Parameter**

```ts
function message(msg?: string){
    if(msg) {
        console.log(msg);
    } else {
        console.log("No message provided");
    }
}
// message("Hello World")
```

> **Optional interface property**

```ts
interface House {
    room: number;
    price: number;
    garage?: number;
}
const house1 : House = {
    room: 4,
    price: 300000
}
```

> **?? opérateur**

```ts
const data = "";
const display = data ?? "Hello World"
console.log(display);

// Never

function alertUser(msg: string): never {
    throw msg;
}
alertUser("Alerte, comportement dangereux")
```

## 3- Overload

```ts
type NumberOrString = number | string;

function combine(a: number, b: number): number
function combine(a: number, b: string): string
function combine(a: string, b: number): string
function combine(a: string, b: string): string
function combine(a: NumberOrString, b: NumberOrString){
    if(typeof a === "string" || typeof b ==="string") {
        return a.toString() + b.toString()
    } else {
        return a + b;
    }
}
console.log(combine(50, 1));
```

## 4- Les Generics

> **Interface Reutilisable**

```ts
interface City<T> {
    name: string, 
    pop: number,
    additionalData: T
}
const Londres: City<object> = {
    name: "Londres",
    pop: 10,
    additionalData: {area: 1572}
}
const Paris: City<object[]> = {
    name: "Paris",
    pop: 5,
    additionalData: [{underground: true, lines: 57}, {restaurant: true
```

> **Generics with functions**

```ts
const addRepairDate = <T extends object> (obj: T) => {
    const lastRepair = new Date()
    return {...obj, lastRepair}
}

const auto1 = addRepairDate({model: "A1", km: 70000, price: 10000})
const auto2 = addRepairDate({model: "A1", km: 70000, price: 10000, color: "white"})
console.log(auto1.model);
```

