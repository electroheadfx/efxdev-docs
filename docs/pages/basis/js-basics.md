# Javascript basics

#### `html` DOM creation

> create HTML elements and element content

```js
<script>
      document.getElementById('title').innerHTML = 'Welcome!'
      //h2
      var newH2 = document.createElement('h2')
      newH2.innerHTML = 'Introduction'
      //add h2 to root
      var rootDiv = document.getElementById('root')
      rootDiv.appendChild(newH2)

      //add p to root
      var newP = document.createElement('p')
      newP.innerHTML = 'Ceci est un paragraphe'
      rootDiv.appendChild(newP)

      //add footer to root
      var newFooter = document.createElement('footer')
      newFooter.innerHTML = 'Site créé par ..'
      rootDiv.appendChild(newFooter)
    </script>
```

> Create attributes
> 
> ```js
> <!DOCTYPE html>
> <html>
>   <body>
>     <div id="root">
>       <h1 id="title">Hello World</h1>
>     </div>
>     <script>
>       var rootDiv = document.getElementById('root')
> 
>       var styleAttr = document.createAttribute('style')
>       styleAttr.value = 'background-color:powderblue;'
>       rootDiv.setAttributeNode(styleAttr)
>     </script>
>   </body>
> </html>
> ```

#### `for` loop in array<sup>*</sup>

```js
var langageList = ['html', 'css', 'js']
for (var i = 0; i < langageList.length; i++) {
   console.log(langageList[i])
}
```

> *we use ES6 functionnal programming now with map, find, filter ...

#### `Splice` for array

```js
// remove last element in array
langageList.splice(langageList.length - 1)
```

- [Mozilla splice Docs]([JavaScript Array splice() Method](https://www.w3schools.com/jsref/jsref_splice.asp)

#### `Object` Docs

- [JavaScript Objects Docs](https://www.w3schools.com/js/js_objects.asp)

- [for...in - JavaScript Docs](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Statements/for...in)

```js
for (var key in personne) {
  console.log(key)
}
```

#### `include` test an array inside object

```js
var personne = {
   nom: 'Chirac',
   langages: ['html', 'css', 'js'],
}

if (personne.langages.includes('js')) {
  console.log('condition langages est ok')
} else {
  console.error('condition langages est ko')
}
```

# Pop, Push, Shift and Unshift Array Methods in JavaScript

JavaScript gives us four methods to add or remove items from the beginning or end of arrays:

### **pop()**: Remove an item from the end of an array

```js
let cats = ['Bob', 'Willy', 'Mini'];

cats.pop(); // ['Bob', 'Willy']
```

*pop()* returns the removed item.

### **push()**: Add items to the end of an array

```js
let cats = ['Bob'];

cats.push('Willy'); // ['Bob', 'Willy']

cats.push('Puff', 'George'); // ['Bob', 'Willy', 'Puff', 'George']
```

*push()* returns the new array length.

### **shift()**: Remove an item from the beginning of an array

```js
let cats = ['Bob', 'Willy', 'Mini'];

cats.shift(); // ['Willy', 'Mini']
```

*shift()* returns the removed item.

### **unshift()**: Add items to the beginning of an array

```js
let cats = ['Bob'];

cats.unshift('Willy'); // ['Willy', 'Bob']

cats.unshift('Puff', 'George'); // ['Puff', 'George', 'Willy', 'Bob']
```

*unshift()* returns the new array length.
