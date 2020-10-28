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

Une boîte est prête pour stocker la valeur nommée "message". Maintenant nous pouvons spécifier dans notre script qui faire avec le "message", par exemple de mettre message en majuscule et l'afficher sur l'écran. Ce qui sera afficher changera en fonction de la valeur stockée dans la boîte "message".

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

---

## Exercices

[javascript quizzes - variables (1)](https://javascript-quizzes.netlify.app/variables-1)

