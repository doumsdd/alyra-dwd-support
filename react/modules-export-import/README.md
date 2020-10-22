# modules, export,  import

Jusqu'ici nous avons utilisé les fichiers `js` comme ceci :

```html
<!DOCTYPE="html">
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
'use strict'
const gradients = [{start: red, end: magenta}]
```

`script2.js` est inclu après `script1.js` alors

```javascript
/* script1.js */
'use strict'
console.log(gradients.length)
// 1
```

Il est aussi possible d'utiliser des fichiers JavaScript en tant que des *modules*.

```html
<!DOCTYPE="html">
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
const gradients = [{start: red, end: magenta}]
```

`script2.js` est inclu après `script1.js` alors

```javascript
/* script1.js */
console.log(gradients.length)
// Uncaught ReferenceError: gradients is not defined
```

 - modules sont toujours en mode `strict`, on a plus besoin de spécifier : `use strict`
 - modules ont leur propre scope
 
https://codepen.io/alyra/pen/vYGxebw

## export & import 

Si modules ont leur propre scope, comment utiliser les variables et fonctions définies dans un autre modules ? 

<strong>Modules échangent des fonctionnalités avec des directives `export` et `import`.</strong>

### *named exports*

Voici comment nous exposons des variables mises en place dans le fichier `gradients.js`:

```javascript
/* gradients.js */
export const gradients = [
  {
    name: "Grade Grey",
    start: "rgb(189, 195, 199)",
    end: "rgb(44, 62, 80)",
    tags: ["gris"]
  },
  {
    name: "Harvey",
    start: "rgb(31, 64, 55)",
    end: "rgb(153, 242, 200)",
    tags: ["vert"]
  }
]
export const uniqueTags = ["gris", "vert"]
```

et voici comment nous les recupérons dans `GradientsList.js`:

```javascript
/* GradientsList.js */
import {gradients, uniqueTags} from './path/to/gradients.js'
```

Il est aussi possible de renommer la variable importée :

```javascript
/* GradientsList.js */
import {gradients as myGradients, uniqueTags} from './path/to/gradients.js'
```

### *default* exports

À côté des *named exports*, nous avons aussi *default exports.*
Chaque module peut avoir au maximum un *export default.*

Voici comment exposer la variable :
 
```javascript
/* GradientsList.js */ */
const GradientsList = (props) => {...}
export default GradientsList
```

et comment la récuperer (un détails clé, ici nous n'avons pas des accolades).

```javascript
/* App.js */
import GradientsList from "./path/to/GradientsList.js"
```

Dans ce cas là, nous pouvons nommer librement notre variable importée, le suivant marcherait également :

```javascript
/* App.js */
import Gradients from "./path/to/GradientsList.js"
```

## Vous pouvez en lire davantage :

- [ressources - modules](https://javascript.info/modules-intro)
- [ressources - export/import](https://javascript.info/import-export)
