# Functions

Fonctions permettent d'englober les parties du code afin de les rendre **reutilisables** et **paramétrables**.  
Imaginons que nous avons un petit script qui permet de vérifier si l'identifiant d'utilisateur a un format correct. Pour qu'un identifiant utilisateur puisse être enregistrer dans notre base de données il doit être tout en minuscules avec un maximum de 8 caractères.

```javascript
let userName = "paulina"
let ok
if (userName.length > 8) {
  console.log("Cet identifiant est trop longue")
  ok = false
} else if {
  userName.toLowerCase() !== userName
  console.log("Cet identifiant contient des majuscules")
  ok = false
} else {
  console.log("Le système valide votre identifiant 👍")
  ok = true
}

// et ensuite ...
if (ok) {
  // l'identifiant est ajouté dans la base de données
}
```

Afin de vérifier la validité d'un autre identifiant nous devons repeter le même code :

```javascript
userName = "Alyra"
if (userName.length > 8) {
  console.log("Cet identifiant est trop longue")
  ok = false
} else if {
  userName.toLowerCase() !== userName
  console.log("Cet identifiant contient des majuscules")
  ok = false
} else {
  console.log("Le système valide votre identifiant 👍")
  ok = true
}

// et ensuite ...
if (ok) {
  // l'identifiant est ajouté dans la base de données
}

userName = "alyra2021"
if (userName.length > 8) {
  console.log("Cet identifiant est trop longue")
  ok = false
} else if {
  userName.toLowerCase() !== userName
  console.log("Cet identifiant contient des majuscules")
  ok = false
} else {
  console.log("Le système valide votre identifiant 👍")
  ok = true
}

// et ensuite ...
if (ok) {
  // l'identifiant est ajouté dans la base de données
}
```

et ainsi de suite...

Une fonction nous permettra de convertir notre script en un "block" réutilisable.

```javascript
function verifyUserName(userName) {
  let ok
  if (userName.length > 8) {
    console.log("Cet identifiant est trop longue");
    ok = false;
  } else if (userName.toLowerCase() !== userName) {
    console.log("Cet identifiant contient des majuscules");
    ok = false;
  } else {
    console.log("Le système valide votre identifiant 👍");
    ok = true;
  }
  return ok;
}

if (verifyUserName("paulina")) {
  // l'identifiant est ajouté dans la base de données
}
if (verifyUserName("Alyra")) {
  // l'identifiant est ajouté dans la base de données
}
if (verifyUserName("alyra2021")) {
  // l'identifiant est ajouté dans la base de données
}
```

![](https://wptemplates.pehaa.com/assets/alyra/function.png)



## déclaration

Que vient de se passer ? Nous venons de déclarer une fonction, la fonction `verifyUserName` (lignes 1 - 15 dans l'image ci-dessus). 
Afin de déclarer une fonction nous :
- utilisons un mot-clé spécial `function`
- suivie par l'identifiant que nous avons choisi pour notre fonction (la convention camelCase s'applique toujours)
- ensuite viennent des parenthèses, leur rôle est de passer des paramètres
- esuite des accoulades entourent le *body* de notre fonction
- le mot-clé spécial `return` renvoie le résultat de notre fonction, l'exécution de notre fonction s'arrête

```javascript
function nomDeFonction(param1, param2) {
  ...
  return ...
}
```

Afin **d'appeler la fonction** (ligne 17 l'image ci-dessus) nous utilisons son identifiant avec les paramètres entre les parenthèses `verifyUserName("paulina")` est égale à ce qui est renvoyé par la fonction (ce qui suit le mot-clé `return`). Une fonction peut aussi génére ce qu'on appele des *side effects* (effets de bord), par exemple envoyer des alerts, des message dans la console, faire des connections network (nous allons apprendre !), enregistrer des information dans le stockage interne de navigateur etc.

**Est-ce possible d'avoir une fonction sans paramètres ?** Tout à fait. Dans ce cas-là nous laissons les paramètres vides, voici un exemple :

```javascript
function todayDayName() {
  const day = new Date().getDay()
  switch (day) {
    case 1:
      return "lundi"
    case 2:
      return "mardi"
    case 3:
      return "mercredi"
    case 4:
      return "jeudi"
    case 5:
      return "vendredi"
    case 5:
      return "samedi"
    default:
      return "dimanche"
  }
}
```

**Est-ce possible d'avoir une fonction avec plusieurs paramètres ?**

Voici une fonction avec 2 paramètres :

```javascript
function betterPassword(string1, string2) {
  if (string1.length > string2.length) {
    return string1
  } else {
    return string2
  }
}

betterPassword("alyra2021", "alyraParis2021")
// "alyraParis2021"
// attention, c'est un exemple trop simpliste, dans la pratique la longueur n'est pas le seul critère pour la force d'un mot de passe
```

Il est très important de comprendre que **`return` arrête l'execution de la fonction**

```javascript
function cube(number) {
  const answer = number * number * number
  return answer
  /* console.log ne sera jamais executé */
  console.log(anser)
}
```

En sachant que `return` arrête l'exection, nous pouvons re-ecrire `verifyUserName`

```
function verifyUserName(userName) {
  if (userName.length > 8) {
    console.log("Cet identifiant est trop longue");
    return false
  }
  if (userName.toLowerCase() !== userName) {
    console.log("Cet identifiant contient des majuscules");
    return false
  }
  console.log("Le système valide votre identifiant 👍");
  return true
}
```

---

Il est possible qu'une fonction n'a pas de `return`. Dans ce cas-là juste avant la fermeture des accolades, `return udefined` est ajouté de la façon implicite par JavaScript.

```javascript
function showMessage() {
  let message = "Bonjour Alyra !"
  alert(message)
}

/*
function showMessage() {
  let message = "Bonjour Alyra !"
  alert(message)
  return undefined
}
*/

const output = showMessage() // affiche "Bonjour Alyra !"
console.log(output) // undefined
```

---

## Variables locales & globales, scope

```javascript
function showMessage() {
  let message = "Bonjour Alyra !" // variable locale
  alert(message)
}

showMessage() // affiche "Bonjour Alyra !"
alert(message) // Error !
```

Vous vous l'appelez que les variables dans JavaScript sont visible dans leur "scope".
Le "scope" de `let` et `const` est un block (pour `var` c'est function).

Une fonction a accès aux variables extérieures (outer).

```javascript
"use strict"
let message = "Bonjour Alyra !" // variable globale
function showMessage() {
  console.log(message)
}

showMessage() // affiche "Bonjour Alyra !"
console.log(message) // affiche "Bonjour Alyra !"
```

Une fonction peut aussi modifier la variable globale, comme ci-dessous :

```javascript
"use strict"
let message = "Bonjour Alyra !" // variable globale
function showMessage() {
  message = "Hello World!"
  console.log(message)
}

console.log(message) // affiche "Bonjour Alyra !"
showMessage() // affiche "Hello World!"
console.log(message) // affiche "Hello World!"
```

Il faut savoir que la variable globale **va être utilisée uniquement s'il n'y a pas de variable locale avec le même nom.**
Nous pouvons dans la fonction déclarer une variable avec le même nom qu'une variable globale. Dans ce cas la variable locale est utilisée (on appelle ça parfois _shadowing_). Ce serait plus simple à analyser avec les exemples :

```javascript
let message = "Bonjour Alyra !" // variable globale
function showMessage() {
  let message = "Hello World!"
  console.log(message)
}

console.log(message) // affiche "Bonjour Alyra !"
showMessage() // affiche "Hello World!"
console.log(message) // affiche "Bonjour Alyra !"
```

L'argument d'une fonction est une variable dans son "local scope".

```javascript
let message = "Bonjour Alyra !" // variable globale
function showMessage(message) {
  message += "!"
  console.log(message)
}

console.log(message) // affiche "Bonjour Alyra !"

showMessage("Hello World") // affiche "Hello World!"

console.log(message) // affiche "Bonjour Alyra !"
```

![](https://assets.codepen.io/4515922/input.png)
![](https://assets.codepen.io/4515922/output.png)

## Function expressions

```javascript
const minimum = function (param1, param2) {
  if (param1 < param2) {
    return param1
  }
  return param2
}

minimum(-10, -4)
// -10
```

```javascript
const minimum = function (param1, param2) {
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
const square = (x) => x * x

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
const minimum = (param1, param2) => (param1 < param2 ? param1 : param2)

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

- [js quizzes - Functions](https://javascript-quizzes.netlify.app/functions)
- [Functions - Numbers](https://codepen.io/alyra/pen/eYJEwrO) | [solution](https://codepen.io/alyra/pen/abaea20f1823c94978546278d1a4a061)
- [Functions - Strings](https://codepen.io/alyra/pen/LYGjwgr) | [solution](https://codepen.io/alyra/pen/2c45a0d1cb435599d910b9a042a00a39)
- [Functions (3)](https://codepen.io/alyra/pen/pogxdzK) | [solution](https://codepen.io/alyra/pen/017b258bdaa4e071e83b34f9f73b9410)
