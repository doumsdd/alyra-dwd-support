# Variables

Une variable est un «stockage nommé» pour les données.

Nous les avons déjà vu dans sass (comme ci-dessous 👇)

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

![](https://assets.codepen.io/4515922/message.png)

```javascript
let message = "Bonjour"
```

![](https://assets.codepen.io/4515922/message1.png)

```javascript
let message = "Bonjour"
message = "Hello World"
```

![](https://assets.codepen.io/4515922/message2.png)

```javascript
let message = "Hello World"
message += "!"
// message devient "Hello World!"
```

![](https://assets.codepen.io/4515922/message3.png)

```javascript
let message = "Hello World"
// 🚫 ceci n'est pas correcte !!!
let message = "Bonjour"
```

<div style="display: flex">
  <div class="box-variable with-value shake">
    <span class="variable">message</span>
    <span class="value">"Hello World"</span>
  </div>
  <div class="box-variable with-value">
    <span class="variable">message</span>
    <span class="value">"Bonjour"</span>
  </div>
 </div>
 
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

Il est important de savoir qu'il existe aussi le mot-clé `var` qui permet de déclarer les variables. C'était la seule possibilité avant l'arrivée de ES6 (ECMAScript 6, ECMAScript 2015).

---

Les `;` à la fin de chaque ligne ne sont pas obligatoire. JavaScript considere (avec quelques rares exceptions) que la ligne finit par un `;`</p>

Le nom d'une variable (son identifiant) peut contenir des lettres majuscules ou minuscules, des chiffres (sauf en première position) et certains caractères comme le dollar `$` ou underscore `_`.
