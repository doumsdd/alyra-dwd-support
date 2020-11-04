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

Nous venons d'attribuer une valeur à notre variable. Cette opération s'appelle **"affectation".**

Il est possible de remplacer la valeur stockée sous le nom "message".

```javascript
let message = "Bonjour"
// un peu plus tard dans notre script on affecte "Hello World", la valeur de message change
message = "Hello World"
```

![](https://assets.codepen.io/4515922/message2.png)

Voici comment nous pouvons modifier la valeur au lieu de la remplacer :
```javascript
let message = "Hello World"
message += "!"
// message devient "Hello World!"
```

L'opération que nous venons d'effectuer `message += "!"` joint affectation et addition et s'appelle en fait **"affectation après addition"**. 
Elle est équivalente à :

```javascript
message = message + "!"
// message += "!"
```

Nous ne sommes pas limités à l'opération "+=", il existe aussi **affectation après soustraction,** **affectation après multiplication** etc.

```javascript
let price = 100
const discount = 20
price -= discount
// price = price - discount
```

```javascript
let price = 100
const percentDiscount = 0.2
price *= 1 - percentDiscount
// price = price * (1 - percentDiscount)
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

**Attention,** il n'est pas possible de "re-déclarer" la variable.

![](https://assets.codepen.io/4515922/message3.png)

```javascript
let message = "Hello World"
// 🚫 ceci n'est pas correcte !!! la boîte message existe déjà !!
let message = "Bonjour"
```
 
Il est aussi possible de déclarer une variable avec un *mot-clé* `const` (et pas `let`). Dans ce cas-là nous n'avons pas le droit de modifier sa valeur. 
 
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

Il est important de savoir qu'il existe aussi le troisième mot-clé permettant de déclarer une variable : `var`. Il était remplacé par `let` et `const` avec l'arrivée d'ECMAScript 2015. L'utilisation de `var` est en déclin. Vous allez sans doute le voir dans multiples ressources qui n'étaient pas encore re-adapté à ECMAScript 2015. Mais nous n'allons jamais l'utiliser.

---

## Noms de variables

Peut-on appeler une variable librement ? Presque, il existe pourtant quelques limitations.
Le nom d'une variable (son identifiant) peut contenir des lettres majuscules ou minuscules, des chiffres (sauf en première position) et certains caractères comme le dollar `$` ou underscore `_`.

Les noms de variables sont sensibles à la casse : `firstName`, `firstname`, `FirstName` et `FIRSTNAME` correspondraient aux 4 variables différentes. 
Le format *camelCase* (`firstName`) est fortement privilégié.

Il existe aussi quelques mots-clés spéciaux qui ont leur propre signification dans JavaScript et ne peuvent pas être utilisés en tant que noms des variables. Vous trouverez la liste des mots interdits [ici.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)

## Fin de la ligne (`;`)

Les `;` à la fin de chaque ligne ne sont pas obligatoires. JavaScript considère (avec quelques rares exceptions) que la ligne finit par un `;`


## Mode strict

Le mode strict a été introduit avec la version ECMAScript 5 qui proposait JavaScript plus restrictif, plus sécurisé, avec quelques changements dans la syntaxe et plusieurs optimisations. En particulier, avec ECMAScript 5 certaines erreurs "silencieuses" deviennent des erreurs explicites (qui peuvent arrêter l'exécution des scripts). Afin de mettre en place une nouvelle version, sans compromettre les scripts existantes, l'instruction `"use strict"` a été proposé. Si la directive `"use strict"` est trouvée au début du script, la version restrictive de JavaScript est servie.

À partir de ce moment, nous allons commencer nos scripts avec cette directive.

## Exemples :

Forkez et clonez [ce repo,](https://github.com/pehaa/js-start) ensuite ouvrez le projet dans VSCode est lancez Live Server.

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
    <p>Dans cet exemple, le navigateur te demandera ton prénom afin de te saluer "Hello ! Ravi de te rencontrer, ...."</p>
    <p>Pour l'interaction navigateur-utilisateur, nous utilisons des méthodes <code>alert</code> et <code>prompt</code>.</p>
    <script>
      // active mode strict
      // déclare la variable message et affecte la valeur "Hello !"
      // affiche le message
      // déclare la variable name et affecte la valeur d'entrée utilisateur, qui répond à la question 'Comment tu t'appelles ?'
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

Il est recommandé de créer les fichiers JavaScript (avec l'extension `.js`) est l'inclure dans le document HTML avec les balises `script` et l'attribut `src`, comme dans l'exemple suivant :

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
    <!-- écris ton javascript dans un fichier séparé script.js, qui devrait être exécuté ci-dessous -->
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

- [javascript quizzes - variables (1)](https://javascript-quizzes.netlify.app/variables-1)
- [javascript variables - repo ex. restants](https://github.com/pehaa/js-start)

