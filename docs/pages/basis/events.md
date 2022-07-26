# Events in js

> **onclick**

```js
<!DOCTYPE html>
<html>
  <body>
    <div id="root">
      <h1 id="title">Pas d'information</h1>
      <button onclick="handleClick()">Click me</button>
    </div>

    <script>
      function handleClick() {
        var date = new Date().toLocaleDateString()
        var time = new Date().toLocaleTimeString()
        var label = 'Nous sommes le ' + date + ' il est ' + time

        document.getElementById('title').innerText = label
      }
    </script>
  </body>
</html>
```

> **onmouseenter** and **onmouseleave**

```js
<!DOCTYPE html>
<html>
  <body>
    <div id="root">
      <h1 id="title" onmouseover="handleClick()">Pas d'information</h1>
      <button onclick="handleClick()" onmouseover="handleClick()">
        Click me
      </button>
      <div style="background-color: lightblue" onmouseenter="handleClick()">
        entre ici
      </div>
      <div style="background-color: lightcoral" onmouseleave="handleClick()">
        sort d'ici
      </div>
    </div>

    <script>
      function handleClick() {
        var date = new Date().toLocaleDateString()
        var time = new Date().toLocaleTimeString()
        var label = 'Nous sommes le ' + date + ' il est ' + time

        document.getElementById('title').innerText = label
      }
    </script>
  </body>
</html>
```

> **addEventListener** with keydown

Le lien vers la doc [HTML DOM Document addEventListener() Method](https://www.w3schools.com/jsref/met_document_addeventlistener.asp)

```js
<!DOCTYPE html>
<html>
  <body>
    <div id="root">
      <h1 id="title" onmouseover="handleClick()">Pas d'information</h1>
      <button onclick="document.removeEventListener('keydown',handlePress)">
        supprime le listener
      </button>
      <div style="background-color: lightblue" onmouseenter="handleClick()">
        entre ici
      </div>
      <div style="background-color: lightcoral" onmouseleave="handleClick()">
        sort d'ici
      </div>
    </div>

    <script>
      function handleClick() {
        var date = new Date().toLocaleDateString()
        var time = new Date().toLocaleTimeString()
        var label = 'Nous sommes le ' + date + ' il est ' + time

        document.getElementById('title').innerText = label
      }

      function handlePress(event) {
        var name = event.key
        var code = event.code
        console.log('name ' + name + ' : code ' + code)
        if (code === 'Enter' || code === 'ArrowDown ' || code === 'ArrowUp') {
          handleClick()
        }
      }
      //add keydown Listener
      document.addEventListener('keydown', handlePress)
    </script>
  </body>
</html>
```
