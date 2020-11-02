# Modules, export, import

Jusqu'ici nous avons utilisé les fichiers `js` comme ceci :

```html
<!DOCTYPE html>
<html>
  <!-- ... -->
  <body>
    <!-- ... -->
    <script src="script1.js"></script>
    <script src="script2.js"></script>
  </body>
</html>
```

Par exemple:

```javascript
/* script1.js */
"use strict"
const gradients = [{ start: "red", end: "magenta" }]
```

Dans notre fichier HTML, `script2.js` est inclus après `script1.js` alors la variable `gradients` est disponible dans `script2.js`

```javascript
/* script2.js */
"use strict"
// Nous pouvons nous servir de la variable gradients, déclarée dans script1.js
console.log(gradients.length)
// 1
```

---

## JavaScript Modules

Il est aussi possible d'utiliser des fichiers JavaScript en tant que des _modules_.

```html
<!DOCTYPE html>
<html>
  <!-- ... -->
  <body>
    <!-- ... -->
    <script type="module" src="script1.js"></script>
    <script type="module" src="script2.js"></script>
  </body>
</html>
```

```javascript
/* script1.js */
const gradients = [{ start: "red", end: "magenta" }]
```

Même si `script2.js` est inclus après `script1.js`, la variable `gradients` n'est pas disponible dans `script2.js`

```javascript
/* script2.js */
console.log(gradients.length)
// Uncaught ReferenceError: gradients is not defined
```

Voici les 2 choses importantes **à retenir** par rapport aux _modules_ :

- modules **sont toujours en mode `strict`,** on a plus besoin de spécifier : `use strict`
- modules **ont leur propre scope**

https://codepen.io/alyra/pen/vYGxebw

## export & import

Si modules ont leur propre scope, comment utiliser les variables et fonctions définies dans un autre modules ?

<strong>Modules échangent des fonctionnalités avec des directives `export` et `import`.</strong>

### _named exports_

Voici comment nous exposons des variables mises en place dans le fichier `gradients.js`:

```javascript
/* gradients.js */
export const gradients = [
  {
    name: "Grade Grey",
    start: "rgb(189, 195, 199)",
    end: "rgb(44, 62, 80)",
    tags: ["gris"],
  },
  {
    name: "Harvey",
    start: "rgb(31, 64, 55)",
    end: "rgb(153, 242, 200)",
    tags: ["vert"],
  },
]
export const uniqueTags = ["gris", "vert"]
```

et voici comment nous les récupérons dans `GradientsList.js`:

```javascript
/* GradientsList.js */
import { gradients, uniqueTags } from "./path/to/gradients.js"
```

Il est aussi possible de renommer la variable importée :

```javascript
/* GradientsList.js */
import { gradients as myGradients, uniqueTags } from "./path/to/gradients.js"
```

### _default_ exports

À côté des _named exports_, nous avons aussi un _default export._
Chaque module peut avoir un seul _default export._

Voici comment exposer la variable :

```javascript
/* GradientsList.js */
const GradientsList = (props) => {...}
export default GradientsList
```

et comment la récupérer (un détails clé - ici nous n'avons pas des accolades) :

```javascript
/* App.js */
import GradientsList from "./path/to/GradientsList.js"
```

Dans le cas de _default export_, nous pouvons nommer librement notre variable importée, le suivant marcherait également :

```javascript
/* App.js */
import Gradients from "./path/to/GradientsList.js"
```

## Exemple

Nous allons créer un nouveau projet

```bash
mkdir modules-first-steps
```

avec la structure suivante :

```bash
├── app.js
├── gradients.js
└── index.html
```

### gradients.js

```javascript
/* gradients.js */
export const gradients = [
  {
    name: "Grade Grey",
    start: "rgb(189, 195, 199)",
    end: "rgb(44, 62, 80)",
    tags: ["gris"],
  },
  {
    name: "Harvey",
    start: "rgb(31, 64, 55)",
    end: "rgb(153, 242, 200)",
    tags: ["vert"],
  },
]
export const uniqueTags = ["gris", "vert"]
```

### app.js

```javascript
/* app.js */
import { gradients, uniqueTags as tags } from "./gradients.js"
console.log("Gradients :", gradients)
console.log("Unique tags :", tags)
```

### index.html

Remarquez que nous n'incluons pas de fichier `gradients.js`, uniquement `app.js` est inclus.  
L'attribut `type="module"` est indispensable. Son omission provoque une erreur : `Uncaught SyntaxError: Cannot use import statement outside a module`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script type="module" src="app.js"></script>
  </body>
</html>
```

---

## Vous pouvez en lire davantage :

- [ressources - modules](https://javascript.info/modules-intro)
- [ressources - export/import](https://javascript.info/import-export)

