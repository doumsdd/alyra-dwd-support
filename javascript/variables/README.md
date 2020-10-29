# Variables

Une variable est un «stockage nommé» pour les données.  
Nous avons déjà vu des variables dans Sass (comme ci-dessous 👇)

```scss
$brand: tomato;

a {
  color: $brand;
}
button {
  background: $brand;
}
```

ou dans css (👇)

```css
:root {
  --brand: tomato;
}
a {
  color: var(--brand);
}
button {
  background: var(--brand);
}
```

Voici comment nous **déclarons** les variables dans JavaScript :

```javascript
let message
```

Ainsi, nous pouvons imaginer qu'une boîte est prête pour stocker la valeur nommée "message". Maintenant nous pouvons spécifier dans notre script quoi faire avec le "message". Par exemple, nous pouvons mettre message en majuscules et ensuite l'afficher sur l'écran. Ce qui sera affiché changera en fonction de la valeur stockée dans la boîte "message".

![](https://assets.codepen.io/4515922/message.png)

```javascript
let message = "Bonjour"
```

![](https://assets.codepen.io/4515922/message1.png)

Nous allons donc afficher "BONJOUR".

Il est possible de remplacer la valeur stockée sous le nom "message".

```javascript
let message = "Bonjour"
message = "Hello World"
```

Nous allons alors plutôt afficher "HELLO WORLD".

![](https://assets.codepen.io/4515922/message2.png)

Voici comment nous pouvons modifier la valeur au lieu de la remplacer :
```javascript
let message = "Hello World"
message += "!"
// message devient "Hello World!"
```

Notre code complet aurait pu être comme ceci :

```javascript
let message = "Hello World"
message += "!"
// message devient "Hello World!"
message = message.toUpperCase()
// message devient "HELLO WORLD!"
alert(message)
```

Attention, il n'est pas possible de "re-déclarer" la variable.

![](https://assets.codepen.io/4515922/message3.png)

```javascript
let message = "Hello World"
// 🚫 ceci n'est pas correcte !!!
let message = "Bonjour"
```
 
 On peut aussi déclarer les variables "read-only", qu'on ne peut pas modifier. Pour cela on utilise le mot-clé `const`
 
 ```javascript
let message = "Hello"
const name = "Alyra"
message += " " + name
```
![](https://assets.codepen.io/4515922/messagename.png)
 
 ```javascript
const name = "Alyra"
// 🚫 ceci n'est pas correcte !!! 
name = "Cambridge"
```

Il est important de savoir qu'il existe aussi le mot-clé `var` qui permet de déclarer les variables. Son utilisation est en déclin. Il est remplacé par `let` et `const` avec la version de JavaScript référencée comme ES6 (ECMAScript 6 ou ECMAScript 2015).

---

## Noms de variables

Peut-on appeler une variable librement ? Presque, il existe quelques limitations.
Le nom d'une variable (son identifiant) peut contenir des lettres majuscules ou minuscules, des chiffres (sauf en première position) et certains caractères comme le dollar `$` ou underscore `_`.

## Fin de la ligne (`;`)

Les `;` à la fin de chaque ligne ne sont pas obligatoire. JavaScript considere (avec quelques rares exceptions) que la ligne finit par un `;`


## Mode strict

Le mode strict a été introduit avec la version ECMAScript 5 qui proposait JavaScript plus restrictif, plus sécurisé, avec quelques changements dans la syntaxe et plusieurs optimisations. En particulier, avec ECMAScript 5 certaines erreurs "silencieuses" deviennent des erreurs explicites (qui peuvent arrêter l'execution des script). Àfin de mettre en place une nouvelle version, sans compromettre les sripts existantes, l'instruction `"use strict"` à été proposé.

À partir de ce moment, nous allons commencer nos scripts avec cette instruction.

## Exemples :

Forkez et clonez [ce repo](https://github.com/pehaa/js-start) ensuite ouvrez le projet dans VSCode est lancez Live Server.

### Exemple (01)

Nous pouvons mettre le code JavaScript directement dans le document HTML entre les balises `<script>...</script>`.  Dans la plupart de cas les scripts sont attachés juste avant la fermeture de la balise `body`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Bonjour JavaScript 01</title>
  </head>
  <body>
    <h1>Bonjour JavaScript 01</h1>
    <a href="/">retour</a>
    <p>Dans cette exemple, le navigateur te démandera ton prénom afin de te saluer "Hello ! Ravi de te rencontrer, ...."</p>
    <p>Pour l'intéraction navigateur-utilisateur, nous utilisons des méthodes <code>alert</code> et <code>prompt</code>.</p>
    <script>
      // active mode strict
      // déclare la variable message et affecte lui la valeur "Hello !"
      // affiche le message
      // déclare la variable name et affecte lui la valeur d'entrée utilisateur, qui répond à la question 'Comment tu t'appelles ?'
      // personnalise le message en y ajoutant le nom d'utilisateur
      // affiche le message
    </script>
  </body>
</html>
```

Nous allons maintenant écrire notre script :

```javascript
 // active mode strict
 "use strict"
 // déclare la variable message et affecte lui la valeur "Hello !"
 let message = "Hello !"
 // affiche le message
 alert(message)
 // déclare la variable name et affecte lui la valeur d'entrée utilisateur, qui répond à la question 'Comment tu t'appelles ?'
 let name = prompt('Comment tu t'appelles ?)
 // personnalise le message en y ajoutant le nom d'utilisateur
 message += ` Ravi de te connaître ${name} !`
 // affiche le message
 alert(message)
```

### Exemple (04)

Il est recommander de créer les fichiers JavaScript (avec l'extension `.js`) est l'inclure dans le document HTML avec les balises `script` et l'attribut `src`, comme dans l'exemple suivant :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Bonjour JavaScript 04</title>
  </head>

  <body>
    <h1>Bonjour JavaScript 04</h1>
    <a href="/">retour</a>
    <!-- écris ton javascript dans un fichier séparé script.js, qui devrait être executé ci-dessous -->
    <script src="script.js"></script>
  </body>
</html>
```

```javascript
// script.js
/* 
créer la variable answer
demander confirmation 'Confirmez-vous d'être majeur ?' 
affecter la réponse à la variable answer
*/
const answer = confirm('Confirmez-vous d'être majeur ?')
// answer est de type "boolean"
/*
créer la variable message
affecter-lui soit 'Bienvenue !' si la réponse et positive (answer est true) soit  'Vous n'être pas autorisé !' (dans le cas contraire)
Afficher le message
*/
const message = answer ?  'Bienvenue !' : 'Vous n'êtes pas autorisé !'
alert(message)
```

---

## Exercices

[javascript quizzes - variables (1)](https://javascript-quizzes.netlify.app/variables-1)
[javascript variables - repo ex. restants](https://github.com/pehaa/js-start)

