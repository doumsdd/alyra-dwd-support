# Flow : conditions, boucles et *scope*

## Conditions

Dans le code, comme dans la vie, certaines actions ont lieu uniquement dans certaines situations.

### `if`, `if ... else` et `if ... else if ... else`

```javascript
if (🌧) {
  ☂️
}
```

ou on prend des actions différentes selon la situation

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

```javascript
const day = new Date().getDay()
if (day === 1) {
  alert("Pourquoi le lundi est si loin du vendredi, alors que vendredi est si proche du lundi ?")
}
```



### switch

Nous pouvons enchainer `else if` sans limites :


```javascript
const day = new Date().getDay()
if (day === 1) {
  alert("Nous sommes lundi")
} else if (day === 2) {
  alert("Nous sommes mardi")
} else if (day === 3) {
  alert("Nous sommes mercredi")
} else if (day === 4) {
  alert("Nous sommes jeudi")
} else if (day === 5) {
  alert("Nous sommes vendredi")
} else {
  alert("Nous sommes en week-end")
}
```

mais le code ci-dessous n'est pas très lisible. Une des alternatives est la syntaxe de `switch`, voici notre exemple réécrit avec `switch` :

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
    console.log("trop petit 🐥")
  case 4:
    console.log("Exactement !")
  case 5:
    console.log("Trop grand 🦃")
  default:
    console.log("J'ai peur 🙈")
}
/*
Exactement !
Trop grand 🦃
J'ai peur 🙈
*/
```

## Boucles aka Loops 

Les boucles permettent de répéter l'exécution du code jusqu'à certains moments, définis par programmeur. Imaginons un simple jeu de pendu, l'ordinateur va continuer à me demander une lettre jusqu'au moment où soit je gange, soit je perds.

Il y a 3 types de boucles dans JavaScript, la boucle *for*, la boucle *while* et la boucle *do while*.

- `for (begin; condition; step) { body }`,
- `while (condition) { body }`
- `do { body } while (condition)`

Ci-dessous nous allons afficher les nombres de 0 a 5 à trois méthodes

### while

![](https://wptemplates.pehaa.com/assets/alyra/while.png)

```javascript
let i = 0
while (i <= 5) {
  console.log(i)
  i += 1
}
// i = 0
// while (0 <= 5) -> true -> j'entre dans la boucle
// ***** console.log(0) *****
// ***** i = 0 + 1 = 1  *****
// while (1 <= 5) -> true -> je reste dans la boucle
// ***** console.log(1) *****
// ***** i = 1 + 1 = 2  *****
// while (2 <= 5) -> true -> je reste dans la boucle
// ***** console.log(2) *****
// ***** i = 2 + 1 = 3  *****
// while (3 <= 5) -> true -> je reste dans la boucle
// ***** console.log(3) *****
// ***** i = 3 + 1 = 4  *****
// while (4 <= 5) -> true -> je reste dans la boucle
// ***** console.log(4) *****
// ***** i = 4 + 1 = 5  *****
// while (5 <= 5) -> true -> je reste dans la boucle
// ***** console.log(5) *****
// ***** i = 5 + 1 = 6  *****
// while (6 <= 5) -> false -> je n'entre pas dans la boucle
```

Si nous savons afficher le chiffre de 0 à 5, rien ne nous empêche d'afficher les nombres de 0 à 1000, 1000000, etc.
Et si nous savons afficher les nombres, rien nous empêche de faire quelque chose plus utile avec, par exemples calculer leur somme.


```javascript
// 0 + 1 + 2 + .... + 100
// j'initialise sum
let sum = 0
let i = 0
while (i <= 100) {
  console.log(i)
  sum += i
  i += 1  
}
console.log(sum)
// 5050
```


### do while

![](https://wptemplates.pehaa.com/assets/alyra/do_while.png)


```javascript
let i = 0
do {
  console.log(i)
  i += 1
} while (i <= 5)

// i = 0
// j'entre dans la boucle
// ***** console.log(0) *****
// ***** i = 0 + 1 = 1  *****
// while (1 <= 5) -> true -> je reste dans la boucle
// ***** console.log(1) *****
// ***** i = 1 + 1 = 2  *****
// while (2 <= 5) -> true -> je reste dans la boucle
// ***** console.log(2) *****
// ***** i = 2 + 1 = 3  *****
// while (3 <= 5) -> true -> je reste dans la boucle
// ***** console.log(3) *****
// ***** i = 3 + 1 = 4  *****
// while (4 <= 5) -> true -> je reste dans la boucle
// ***** console.log(4) *****
// ***** i = 4 + 1 = 5  *****
// while (5 <= 5) -> true -> je reste dans la boucle
// ***** console.log(5) *****
// ***** i = 5 + 1 = 6  *****
// while (6 <= 5) -> false -> je sors de pas la boucle
```

```javascript
const question = "Choisis un nombre positif"
let answer
do {
  answer = prompt(question)
} while (answer <= 0)
```

### for

![](https://wptemplates.pehaa.com/assets/alyra/for.png)

```javascript
for (let i = 0; i <= 5; i += 1) {
  console.log(i)
}


// begin : i = 0
// 0 <= 5 -> true -> j'entre dans la boucle
// ***** console.log(0) *****
// step : i = 0 + 1 = 1
// 1 <= 5 -> true -> je reste dans la boucle
// ***** console.log(1) *****
// step : i = 1 + 1 = 2
// 2 <= ) -> true -> je reste dans la boucle
// ***** console.log(2) *****
// step : i = 2 + 1 = 3
// 3 <= 5 -> true -> je reste dans la boucle
// ***** console.log(3) *****
// step : i = 3 + 1 = 4 
// 4 <= 5 -> true -> je reste dans la boucle
// ***** console.log(4) *****
// step : i = 4 + 1 = 5 
// 5 <= 5 -> true -> je reste dans la boucle
// ***** console.log(5) *****
// step :  i = 5 + 1 = 6  
// 6 <= 5 -> false -> je sors de pas la boucle
```

## *Breaking the Loop*

Nous pouvons forcer la sortie de la boucle. Pour cela nous utilisons la directive `break` (comme dans `switch`).  
Par exemple :

```javascript
const dinner = "pizza"
let answer 
do {
  answer = prompt("Devine ce que nous avons pour le dinner ?")
  if ( answer === "je n'ai pas faim") break
} while (answer !== dinner)
if (answer === dinner) {
  alert("Tu a deviné!")
}
```

Il est aussi possible de forcer la boucle à aller vers l'itération suivante. 
Par exemple :

```javascript
// la boucle for pour les superstitieux ;)
for (let i = 0; i <= 100; i += 2) {
  if (i === 13) continue
  console.log(i)
}
```

## Scope

Observons ces 2 exemples du code où je programme mes repas (burrito le week-end et salade dans la semaine).
Dans le premier exemple, je déclare la variable `dinner` dans la racine de mon script. Ensuite selon le jour (week-end ou pas) j'affecte une valeur à `dinner`.

```javascript
"use strict"
const day = new Date().getDay()
let dinner
if (day > 5) {
  dinner = "pizza 🍕"
  console.log(`Aujourd'hui c'est ${dinner}.`)
} else {
  dinner = "salade 🥗"
  console.log(`Aujourd'hui c'est ${dinner}.`)
}

console.log(`Tu as aimé ta ${dinner} au dinner ?`)

// "Aujourd'hui c'est salade 🥗."
// "Tu as aimé ta salade 🥗 au dinner ?"
```

Dans le 2e exemple la variable `dinner` est déclarée et la valeur est attribuée en même temps, dans le body de `if` ou `else`.
Que sera-t-il affiché ?

```javascript
"use strict"
const day = new Date().getDay()
if (day > 5) {
  let dinner = "pizza 🍕"
  console.log(`Aujourd'hui c'est ${dinner}`)
} else {
  let dinner = "salade 🥗"
  console.log(`Aujourd'hui c'est ${dinner}`)
}
console.log(`Tu as aimé ta ${dinner} au dinner ?`)
//"Aujourd'hui c'est salade 🥗"
// Uncaught ReferenceError: dinner is not defined at script.js:10
```

`const` et `let` ont la **scope** (portée) limitée au bloc ({...}) dans lequel elles sont déclarées.  
Autrement dit, les variables `const` et `let` ne sont pas "vues" **à l'extérieur** du bloc dans lequel elles sont déclarées.  

On peut utiliser le même nom de variable dans un bloc intérieur, ceci va prendre le dessus (parfois on utilise la notion _shadow_) sur la variable extérieure.

Et maintenant, que sera-t-il affiché ?

```javascript
const day = new Date().getDay()
let dinner = "soupe 🍜"
if (day > 5) {
  let dinner = "pizza 🍕"
  console.log(`Aujourd'hui c'est ${dinner}`)
} else {
  let dinner = "salade 🥗"
  console.log(`Aujourd'hui c'est ${dinner}`)
}
console.log(`Tu as aimé ta ${dinner} au dinner ?`)
//"Aujourd'hui c'est salade 🥗"
//"Tu as aimé ta soupe 🍜 au dinner ?"
```

Comme vous pouvez voir, *scope* d'une variable est important. Une utilisation sans contrôle peut provoquer des erreurs silencieuses qui faussent l'éxecution de votre script. Nous allons revenir à ce sujet prochainement, à l'occasion de l'introduction des fonctions.

## Exercices

- [repo github flow](https://github.com/pehaa/js-flow)
- [variables Alyra lottery](https://codepen.io/alyra/pen/MWKQPzj) | [solution](https://codepen.io/alyra/pen/d2ae034b58871bfa51b4c70e23abcf54)
