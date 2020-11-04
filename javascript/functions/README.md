# Functions

Fonctions permettent d'englober les parties du code afin de les rendre **réutilisables** et **paramétrables**.  
Imaginons que nous avons un petit script qui permet de vérifier si l'identifiant d'utilisateur a un format correct. Nous devons respecter la spécification mise en place dans notre base de données imaginative. Pour qu'un identifiant utilisateur puisse être enregistré dans notre base, il doit être tout en minuscules avec un maximum de 8 caractères.

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

Afin de vérifier la validité d'un autre identifiant, nous devons répéter le même code :

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
```

et encore :

```javascript
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
  // l'identifiant va etre ajouté dans la base de données
}
if (verifyUserName("Alyra")) {
  // l'identifiant va etre ajouté dans la base de données
}
if (verifyUserName("alyra2021")) {
  // l'identifiant va être ajouté dans la base de données
}
```

![](https://wptemplates.pehaa.com/assets/alyra/function.png)



## Déclaration (*function declaration*)

Que vient de se passer ? Nous venons de déclarer une fonction. La fonction `verifyUserName` est déclarée (ceci correspond aux lignes 1 - 14 dans l'image ci-dessus).  
Afin de déclarer une fonction nous :
- utilisons un mot-clé spécial `function`
- suivie par l'identifiant que nous avons choisi pour notre fonction (la convention camelCase s'applique toujours)
- ensuite viennent des parenthèses, leur rôle est de passer des paramètres
- ensuite des accolades entourent le *body* de notre fonction
- le mot-clé spécial `return` renvoie le résultat de notre fonction, l'exécution de notre fonction s'arrête

```javascript
function nomDeFonction(param1, param2) {
  ...
  return ...
}
```

Afin **d'appeler la fonction** (ligne 17 l'image ci-dessus) nous utilisons son identifiant avec les paramètres entre les parenthèses.   `verifyUserName("paulina")` est égal à ce qui est renvoyé par la fonction (ce qui suit le mot-clé `return`). 

Une fonction peut aussi générer ce qu'on appelle des *side effects* (effets de bord), par exemple envoyer des alerts, des message dans la console, faire des connections network (nous allons apprendre !), enregistrer des information dans le stockage interne de navigateur (nous allons apprendre aussi) etc.

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

**Est-ce possible d'avoir une fonction avec plusieurs paramètres ?** Bien sûr.

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
  /* console.log ne sera jamais exécuté */
  console.log(anser)
}
```

En sachant que `return` arrête l'exécution, nous pouvons ré-écrire `verifyUserName`

```javascript
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

```javascript
function betterPassword(string1, string2) {
  if (string1.length > string2.length) {
    return string1
  } 
  return string2
}
```


---

Il est possible qu'une fonction n'a pas de `return`. Dans ce cas-là juste avant la fermeture des accolades, `return undefined` est ajouté de la façon implicite par JavaScript.

```javascript
function showMessage() {
  let message = "Bonjour Alyra !"
  console.log(message)
}

/*
function showMessage() {
  let message = "Bonjour Alyra !"
  console.log(message)
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
  console.log(message)
}

showMessage() // affiche "Bonjour Alyra !"
console.log(message) // Error !
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

Il existe une autre façon de définir une fonction. Nous pouvons affecter une fonction sans nom (anonyme) à une variable. Nous parlons dans ce cas la de *function expression*, voici un exemple :

```javascript
const betterPassword = function (string1, string2) {
  if (string1.length > string2.length) {
    return string1
  } else {
    return string2
  }
}
```

Nous appelons `betterPassword` exactement pareil comme avant :

```javascript
console.log(betterPassword("alyra2021", "alyraParis2021")
```

Un autre exemple :

```javascript
const verifyUserName = function(userName) {
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

console.log(verifyUserName("alyra"))
```

## Arrow function

Avec *function expressions* vient aussi une autre syntaxe, relativement nouvelle, introduite avec ES6. Nous l'appelons *arrow function* ou *function fléchée* en français.


```javascript
const funcName = (param1, param2) => {
  // ....
  return ...
}

/*
// comme
const funcName = function (param1, param2){
  // ...
  return ...
}
*/
```

Si le *body* de notre fonction contient une seule ligne, notre syntaxe peut être encore plus simplifié, nous pouvons nous passes des accolades et le mot-clé `return` :

```javascript
const square = (x) => x * x
const cube = (x) => x * x
console.log(square(2))
// 4
console.log(cube(
```

On peut aller encore un pas plus loin. Si notre fonction a un seul argument, on peut se permettre de ne pas mettre des parenthèses autour du paramètre

```javascript
const square = x => x * x
square(2)
// 4
```

Par contre, si notre fonction prend plusieurs lignes, nous devons utiliser des accolades `{}` et le mot `return` :

```javascript
const square = (x) => {
  console.log(x, x * x)
  return x * x
}
```

```javascript
const betterPassword = (string1, string2) => (string1.length > string2.length ? string1 : string2)

console.log(betterPassword("alyra2021", "alyraParis2021")
// "alyraParis2021"
```

Il existe quelques subtiles différences entre cette syntaxe et *function expression* classique. Nous allons les découvrir un peu plus tard.

## Valeurs par défaut

JavaScript nous donne une très pratique possibilité de définir les valeurs par défaut pour les paramètres des fonctions. 

Voici un exemple :

```javascript
function increment(i = 0, step = 1) {
  return i + step
}
```

Pourquoi est-ce pratique ? Si le paramètre n'est pas passé, sa valeur par défaut est appliquée :

```javascript
console.log(increment())
// i = 0 (par défaut), step = 1 (par défaut)
// 0 + 1 -> 1
console.log(increment(3))
// i = 3, step = 1 (par défaut)
// 3 + 1 -> 4
console.log(increment(5, 2))
// i = 5, step = 2
// 5 + 2 -> 7
```

La même fonction peut être aussi définit comme ceci :

```javascript
const increment = (i = 0, step = 1) => i + step
```

## Exercices

- [js quizzes - Functions](https://javascript-quizzes.netlify.app/functions)
- [Functions - Scope ](https://codepen.io/alyra/pen/QWyZdPo)
- [Functions - Numbers](https://codepen.io/alyra/pen/eYJEwrO) | [solution](https://codepen.io/alyra/pen/abaea20f1823c94978546278d1a4a061)
- [Functions - Strings](https://codepen.io/alyra/pen/LYGjwgr) | [solution](https://codepen.io/alyra/pen/2c45a0d1cb435599d910b9a042a00a39)
- [Functions (3)](https://codepen.io/alyra/pen/pogxdzK) | [solution](https://codepen.io/alyra/pen/017b258bdaa4e071e83b34f9f73b9410)
