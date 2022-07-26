## Binding args example

```js title="bind method with arguments"
function bind(fn, context) {
  return function() {
    fn.apply(context, [...arguments]);
  }
}
```

!!! question

    What is logged to the console?

```js
// use the bind previous function code

const person = {
  name: 'Vishwas'
}

function sayMyName (lastname) {
  console.log(`My name is ${this.name} ${lastname}`);
}

const boundFn = bind(sayMyName, person);
boundFn('Batman');
```

!!! answer

    Line 6 : 'My name is Vishwas Batman'

### Explicit binding example

!!! question

    What is logged to the console?

```js
const person = {
  name: 'Vishwas'
}

function sayMyName () {
  console.log(`My name is ${this.name}`);
}

const sayMyNameVishwas = sayMyName.bind(person)
sayMyNameVishwas ()
```

!!! answer

    Line 6 : My name is Vishwas (Explicit binding)

## Implicit binding example

!!! question

    What is logged to the console?

```js
const person = {
  name: 'Vishwas',
  sayMyName () {
    console.log(`My name is ${this.name}`);
  },
  superHero: {
    name: 'Batman',
    sayMyName () {
      console.log(`My name is ${this.name}`);
    }
  }
}

person.superHero.sayMyName();
```

!!! answer

    Line 4: Batman (implicit binding)