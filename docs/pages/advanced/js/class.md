## Intro

```js title="Person class"
class Person {

  constructor (name) {
    this.name = name;
  }

  sayMyName () {
    console.log( My name is ${this.name} );
  }

  eat (food) {
    console.log( I'm eating ${food}');
  }

  sleep () {
    console.log(’Sleeping’);
  }
}

const vishwas = new Person(’vishwas’);
const batman = new Person(* Batman’);
const superman = new Person(’Superman’);

const vishwas = Person('Vishwas');
vishwas.sayMyName();
// My name is Vishwas

vishwas.eat('pizza');
// I'm eating pizza

vishwas.sleep();
// Sleeping
```

## Exercice

```js title="Calculator and ScientificCalculator class"
class Calculator {

  constructor () {
    this.value = 0;
  }

  add (num) {
    this.value += num;
  }
  subtract (num) {
    this.value -= num;
  }

  print () {
    console.log(this.value);
  }
}

class ScientificCalculator extends Calculator {
  square () {
  	this.value *= this.value;
	}
}
```

```js title="Use the ScientificCalculator class"
const s = new ScientificCalculator();
s.add(10);
s.subtract(5);
s.square();
s.print();
// Logs 25 to the console;

// or write with dot syntax:
s.add(10).subtract(5).square().print();

```