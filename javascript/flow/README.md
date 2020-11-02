# Flow : if, switch, while, for

## Conditions

Dans le code, comme dans la vie, certaines actions ont lieu uniquement dans certaines situations.

### `if`, `if ... else` et `if ... else if ... else`

```javascript
if (🌧) {
  ☂️
}
```

ou on prend des actions différentes selon la situtation

```javascript
if (🌧) {
  ☂️
} else {
  👙
}
```

```javascript
if (🌧) {
  ☂️
} else if (🌥) {
  👖
} else {
  👙
}
```

Après ces 3 exemples "symboliques" nous allons passer au code :

```javascript
const age = prompt("Quel âge as-tu ?")
if (age > 18) {
  alert("Tu peux voter alors")
} else {
  alert("Tu ne peux pas encore voter")
}
```

```javascript
const random = Math.random()
if (random < 0.5) {
  alert("cette fois tu as perdu !")
} else {
  alert("cette fois tu as gagné !")
}
```



### switch

```javascript
const day = new Date().getDay()
switch (day) {
  case 1:
    alert("Nous sommes lundi")
    break
  case 2:
    alert("Nous sommes mardi")
    break
  case 3:
    alert("Nous sommes mercredi")
    break
  case 4:
    alert("Nous sommes jeudi")
    break
  case 5:
    alert("Nous sommes vendredi")
    break
  default:
    alert("Nous sommes en week-end")
}
```

```javascript
const day = new Date().getDay()
let message = ""
switch (day) {
  case 1:
  case 2:
  case 3:
    message = "La semaine commence... 🤩"
    break
  case 4:
  case 5:
    message = "La semaine finit bientôt... 🙃"
    break
  default:
    message = "Nous sommes en week-end !!! 🥳"
}
```

Attention, `break` n'est pas nécessaire un niveau de la syntaxe, mais si on l'oublie, cela a ses conséquences - la suite du code est executée sans vérification de "cas"

```javascript
"use strict"

let a = 2 + 2

switch (a) {
  case 3:
    alert("trop petit 🐥")
  case 4:
    alert("Exactement !")
  case 5:
    alert("Trop grand 🦃")
  default:
    alert("J'ai peur 🙈")
}
```

## Loops

Il y a 3 loops dans JavaScript

- `for (begin; condition; step) { body }`,
- `while (condition) { body }`
- `do { body } while (condition)`

Ci-dessous nous allons afficher les nombres de 0 a 100 à trois méthodes

### while

```javascript
let i = 0
while (i <= 100) {
  console.log(i)
  i++
}
```

```javascript
/* ici on affiche toutes les nombers paires 0, 2, 4, ..., 100 */
let i = 0
while (i <= 100) {
  console.log(i)
  i += 2
}
```

```javascript
const question = "Choisis un nombre positif"
let answer = 1
while (answer <= 0) {
  answer = prompt(question)
}
/* La question n'était pas posée */
```

### do while

```javascript
let i = 0
do {
  console.log(i)
  i++
} while (i <= 100)
```

```javascript
/* ici on affiche toutes les nombers paires 0, 2, 4, ..., 100 */
let i = 0
do {
  console.log(i)
  i += 2
} while (i <= 100)
```

```javascript
const question = "Choisis un nombre positif"
let answer = 1
do {
  answer = prompt(question)
} while (answer <= 0)
/* La question était posée une fois */
```

### for

```javascript
for (let i = 0; i <= 100; i++) {
  console.log(i)
}
```

```javascript
for (let i = 0; i <= 100; i += 2) {
  console.log(i)
}
```

## Scope

```javascript
const day = new Date().getDay()
let dinner
if (day > 5) {
  dinner = "burrito"
} else {
  dinner = "salade"
}

console.log(dinner) // 'burrito' ou 'salade' selon le jour
```

Que sera affiché ?

```javascript
const day = new Date().getDay()
if (day > 5) {
  let dinner = "burrito"
  alert(`Aujourd'hui c'est ${dinner}`)
} else {
  let dinner = "salade"
  alert(`Aujourd'hui c'est ${dinner}`)
}
alert(`Aujourd'hui c'est ${dinner}`)
```

`const` et `let` ont la **scope** (portée) limitée au bloc ({...}) dans lequel elles sont déclarées.  
Les variables `const` et `let` ne sont pas "vues" à l'exterieur du bloc dans lequel elles sont déclarées.  
On peur utiliser le même nom de variable dans un bloc intérieur, ceci va prendre-dessus - _shadow_ la variable extérieure.

Et maintenant, que sera affiché ?

```javascript
const day = new Date().getDay()
let dinner = "soupe"
if (day > 5) {
  let dinner = "burrito"
  alert(`Aujourd'hui c'est ${dinner}`)
} else {
  let dinner = "salade"
  alert(`Aujourd'hui c'est ${dinner}`)
}
alert(`Aujourd'hui c'est ${dinner}`)
```

```
let x = 1

if (x === 1) {
  let x = 2
  console.log(x)
  // ceci affiche ?
}

console.log(x)
// ceci affiche ?
```

## Exercices

- [repo github flow](https://github.com/pehaa/js-flow)
- [variables Alyra lottery](https://codepen.io/alyra/pen/MWKQPzj) | [solution](https://codepen.io/alyra/pen/d2ae034b58871bfa51b4c70e23abcf54)
