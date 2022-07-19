## Filter

![Filter](./images/js/utilities-ES6/filter.png)

### Exemple

> Intial data
```js
const user = {
  "admin": false,
  "user": true,
  "super": true
}
```
#### Output all true data from user object
> Solutions:
```js
Object.keys(user).filter(
  (k) => {
    return user[k]
  }
);
// Output: [ 'user', 'super' ]
```
```js
// shortland version
Object.keys(user).filter(
  (k) => user[k]
);
// Output: [ 'user', 'super' ]
```



## Map

![Map](./images/js/utilities-ES6/map.png)

## Reduce

![Reduce](./images/js/utilities-ES6/reduce.png)

## Exercice with reduce

![Reduce exo](./images/js/utilities-ES6/reduce-exo.png)