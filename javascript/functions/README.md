# Functions

## déclaration

```javascript
function nomDeFonction(param1, param2) {
  ...
  return ...
}
```

```javascript
function minimum(param1, param2) {
  if (param1 < param2) {
    return param1
  } else {
    return param2
  }
}


minimum(10, 4)
// 4
```

![](https://assets.codepen.io/4515922/declaration-appelle.png)

<div class="post-note">
  <p>`return` arrête l'execution de la fonction</p>
</div>

```javascript
function cube(number) {
  const answer = number*number*number
  return answer
  /* console.log ne sera jamais executé */
  console.log(param2)
}
```

```javascript
function minimum(param1, param2) {
  if (param1 < param2) {
    return param1
  } 
  return param2
}
```
 
---

Il est possible qu'une fonction n'a pas de `return`, dans ce cas là, elle retourne `undefined ` par exemple :

```javascript
function showMessage() {
  let message = "Bonjour Alyra !" // variable locale

  alert( message )
}

showMessage() // affiche "Bonjour Alyra !"
const output = showMessage() // affiche "Bonjour Alyra !"
output // undefined
```

---

Comment peut-on écrire la fonction `minimum` différemment ?

```javascript
function minimum(param1, param2) {
  return param1 < param2 ? param1 : param2
}
```

## Variables locales & globales

```javascript
function showMessage() {
  let message = "Bonjour Alyra !" // variable locale

  alert( message )
}

showMessage() // affiche "Bonjour Alyra !"

alert( message ) // Error !
```

Les variables dans JavaScript sont visible dans leur "scope". 
Le "scope" de `let` et `const` est un block (pour `var` c'est function).

Par contre, une fonction peut accèder des variables extérieures (outer)

```javascript
let message = "Bonjour Alyra !" // variable globale
function showMessage() {
  alert( message )
}

showMessage() // affiche "Bonjour Alyra !"

alert( message ) // affiche "Bonjour Alyra !"
```

Une fonction peut aussi modifier la variable globale, comme ci-dessous :

```javascript
let message = "Bonjour Alyra !" // variable globale
function showMessage() {
  message = "Hello World!"
  alert( message )
}

alert( message ) // affiche "Bonjour Alyra !"

showMessage() // affiche "Hello World!"

alert( message ) // affiche "Hello World!"
```

La variable globale va être utilisé uniquement s'il n'y a pas de variable locale avec le même non.

Si dans la fonction on déclare une variable avec le même nom qu'une variable globale, la variable locale est utilisée (on appelle ça parfois *shadowing*) :

```javascript
let message = "Bonjour Alyra !" // variable globale
function showMessage() {
  let message = "Hello World!"
  alert( message )
}

alert( message ) // affiche "Bonjour Alyra !"

showMessage() // affiche "Hello World!"

alert( message ) // affiche "Bonjour Alyra !"
```

L'argument d'une fonction est une variable dans son "local scope"

```javascript
let message = "Bonjour Alyra !" // variable globale
function showMessage(message) {
  message += "!"
  alert( message )
}

alert( message ) // affiche "Bonjour Alyra !"

showMessage("Hello World") // affiche "Hello World!"

alert( message ) // affiche "Bonjour Alyra !"
```

![](https://assets.codepen.io/4515922/input.png)
![](https://assets.codepen.io/4515922/output.png)

## Function expressions

```javascript
const minimum = function(param1, param2) {
  if (param1 < param2) {
    return param1
  } 
  return param2
}

minimum(-10, -4)
// -10
```

```javascript
const minimum = function(param1, param2) {
   return param1 < param2 ? param1 : param2
}

minimum(-10, -4)
// -10
```


## Arrow function

```javascript
const funcName = (arg1, arg2, ...) => expression retournée
```

```javascript
const square = (x) => x * x

square(2)
// 4
```

S'il y a qu'un seul argument, on peut se permettre à ne pas mettre des parenthèses

```javascript
const square = x => x * x

square(2)
// 4
```

Si notre expression doit prendre plusieur lignes, nous devons utiliser des accolades `{}` et le mot `return`


```javascript
const square = (x) => {
  console.log(x, x * x)
  return x * x
}
```


```javascript
const minimum = (param1, param2) => param1 < param2 ? param1 : param2

minimum(-10, -4)
// -10
```

Parfois, le code peut être plus lisible si nous gardons les accolades et `return`

```javascript
const minimum = (param1, param2) => {
   return param1 < param2 ? param1 : param2
}

minimum(-10, -4)
// -10
```


## Valeurs par défaut


```javascript
function increment(i = 0, step = 1) {
  return i + step
}

increment()
// 1
increment(3)
// 4
increment(5, 2)
// 7
```

```javascript
const increment = (i = 0, step = 1) => i + step

increment()
// 1
increment(3)
// 4
increment(5, 2)
// 7
```

## Exercices

- [js quizzes - Functions](https://javascript-quizzes.vercel.app/functions)
 - [Functions  - Numbers](https://codepen.io/alyra/pen/eYJEwrO) | [solution](https://codepen.io/alyra/pen/abaea20f1823c94978546278d1a4a061)
 - [Functions - Strings](https://codepen.io/alyra/pen/LYGjwgr) | [solution](https://codepen.io/alyra/pen/2c45a0d1cb435599d910b9a042a00a39)
 - [Functions (3)](https://codepen.io/alyra/pen/pogxdzK) | [solution]( https://codepen.io/alyra/pen/017b258bdaa4e071e83b34f9f73b9410)