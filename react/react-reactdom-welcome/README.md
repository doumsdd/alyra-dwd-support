# React et ReactDOM - welcome !!

React est une librarie JavaScript créé et maintenu par Facebook.

Le rôle de React est de faciliter la création des interfaces utilisateur (UI).

Afin de travailler avec React nous avons besoin de 2 fichiers source :

- **React** [https://unpkg.com/react/umd/react.development.js](https://unpkg.com/react/umd/react.development.js)
- **ReactDOM** [https://unpkg.com/react-dom/umd/react-dom.development.js](https://unpkg.com/react-dom/umd/react-dom.development.js)

# React.createElement + ReactDOM.render

```javascript
// créer un élément
const element = React.createElement(
  type,
  [props],
  [...children]
)
// l'insérer/mettre à jour dans domCointainer
ReactDOM.render(
  element, //reactElement
  domContainer // DOM Element
)
```

Commençons notre aventure avec React par la comparaison de deux approches :

 - création d'interface utilisateur avec DOM
 - création d'interface utilisateur avec React et ReactDOM
 
[[[pen slug-hash='PoNGGJM' height='300' theme-id='1']]]
 
# Exemples

```javascript
const element = React.createElement("p")
ReactDOM.render(element, document.getElementById("root"))
// <p></p>
```

```javascript
const element = React.createElement(
  "h1",
  null, // ou {}
  "Je suis le titre"
)
ReactDOM.render(element, document.getElementById("root"))
// <h1>Je suis le titre</h1>
```

```javascript
const element = React.createElement(
  "h1",
  {
    className: "display-1",
    lang: "en",
    id: "top"
  },
  "Hello World!"
)
ReactDOM.render(element, document.getElementById("root"))
// <h1 class="display-1" lang="en" id="top">Hello World!</h1>
```

```javascript
const element = React.createElement(
  "h1",
  {
    className: "display-1",
    lang: "en",
    id: "top",
    children: "Hello World!"
  }
)
ReactDOM.render(element, document.getElementById("root"))
// <h1 class="display-1" lang="en" id="top">Hello World!</h1>
```

```javascript
const element = React.createElement(
  "p",
  {
    className: "lead"
  },
  "Bonjour le Monde !", 
  " Notre aventure avec React commence."
)
ReactDOM.render(element, document.getElementById("root"))
// <p class="lead">Bonjour le Monde ! Notre aventure avec React commence.</p>
```

```javascript
const element = React.createElement(
  "p",
  {
    className: "lead",
    children: ["Bonjour le Monde !", " Notre aventure avec React commence."]
  }
)
ReactDOM.render(element, document.getElementById("root"))
// <p class="lead">Bonjour le Monde ! Notre aventure avec React commence.</p>
```

```javascript
const element = React.createElement(
  "article",
  {
    className: "card"
  },
  React.createElement("h2", null, "Secrets des pandas roux"),
  React.createElement("img", {src: "panda-roux.png", alt: "Panda roux dort sur une branche."}),
  React.createElement("p", null, "Le petit panda est un carnivore, qui ne mange jamais de la viande.")
)
ReactDOM.render(element, document.getElementById("root"))
/*
<article class="card">
  <h2>Secrets des pandas roux</h2>
  <img src="panda-roux.png" alt="Panda roux dort sur une branche.">
  <p>Le petit panda est un carnivore, qui ne mange jamais de la viande.</p>
</article>
*/
```

# ReactDOM.render

[[[pen slug-hash='PoNZvgd' height='300' theme-id='1']]]

Si l’élément React était déjà affiché dans container, `ReactDOM.render` utilise un algorithme de différence DOM de React (diffing algorithm) afin de modifier le DOM uniqument où c’est strictement nécessaire pour refléter la mise à jour de l’élément React.

# React.Fragment

Dans tous les exemples ci-dessus, nous avant **un** élément parent qui a un ou plusieurs noeuds enfants. Afin d'avoir des "siblings" (👭) nous devons utiliser `React.Fragment`, un conteneur sans type ni attribut. Un conteneur phantôme 👻

```javascript
const element = React.createElement(
  React.Fragment,
  null,
  React.createElement("h1", {lang: "en"}, "Hello World!"),
  React.createElement("p", {className: "subtitle"}, "Les premiers mots d'un logiciel"),
)
/*
<h1 lang="en">Hello World!</h1>
<p class="subtitle">Les premiers mots d'un logiciel</p>
*/
```

on peut bien sûr affecter des éléments React aux variables

```javascript
const h1 = React.createElement(
  "h1", 
  {lang: "en"}, 
  "Hello World!"
)
const p = React.createElement(
  "p",
  {className: "subtitle"}, 
  "Les premiers mots d'un logiciel"
)
const element = React.createElement(
  React.Fragment,
  null,
  h1,
  p
)
/*
<h1 lang="en">Hello World!</h1>
<p class="subtitle">Les premiers mots d'un logiciel</p>
*/
```


**Petite digression :** En fait, [*fragment* existe aussi dans le DOM.](https://developer.mozilla.org/fr/docs/Web/API/DocumentFragment) Voici un exemple de son utilité :

```javascript
const ul = document.getElementById("my-shopping-list")
const fragment = document.createDocumentFragment()
for (let item of ['miel', 'sel', 'cumin', 'curry']) {
  const li = document.createElement('li')
  li.textContent = item
  // ul.append(li) <- pas comme ceci puisque layout est "recalculé" à chaque passage de la boucle 
  fragment.append(li) // n'affecte pas le layout
}

ul.append(fragment) // yes ! tous les nouveaux noeuds sont ajoutés une seule fois
```

## Les attributs

Dans la majorités des cas, on utilise des attributs de la même façon que dans HTML. Il y a pourtant quelques exceptions, voici quelques exemples :

- on ne l'utilise pas l'attribut HTML `class` mais `className`

```javascript
const element = React.createElement(
  "h1",
  {
    className: 'display-1 text-center'
  },
  "Bienvenue et bonne journée !!"
);
```



- on ne l'utilise pas l'attribut HTML `for` (`label`) mais 'htmlFor`

```javascript
React.createElement(
  'label', 
  {
    htmlFor: "mail"
  },
  "Votre adresse e-mail"
}
```

- la valeur de l'attribut `style` n'est plus un string mais un object

```javascript
const element = React.createElement(
  "h1",
  { 
    style: {
      letterSpacing: '2px',
      color: 'magenta'
    } 
  },
  "Bienvenue et bonne journée !!"
);
```

**Attention** 

- aux nom des propriétés en camelCase et les valeurs avec des guillemets
- `!important` ne marche pas avec le style inline dans React

---

## Exercices :

 - [React.createElement - p](https://codepen.io/alyra/pen/mdProPw) | [solution](https://codepen.io/alyra/pen/996c540d3b4910dd8e7f44a09bd4bbc9)
 - [React.createElement - button](https://codepen.io/alyra/pen/jOqMJZJ) | [solution](https://codepen.io/alyra/pen/c2fbab1869a4e5a3e42180cf8ac203ef)
 - [React.createElement - h1](https://codepen.io/alyra/pen/rNeMRRx) | [solution](https://codepen.io/alyra/pen/269e8a2880caa3e09477d603577244c7)
 - [React.createElement - input](https://codepen.io/alyra/pen/RwagEMo) | [solution](https://codepen.io/alyra/pen/a00f3fe1653bcff33b3e57a5bd1e1c66)
 - [React.createElement - header](https://codepen.io/alyra/pen/RwagEBK) | [solution](https://codepen.io/alyra/pen/25ecf36755944b625fcf2dd9a5f715ac)
 - [React.createElement - label + input](https://codepen.io/alyra/pen/yLOXZJd) | [solution](https://codepen.io/alyra/pen/6d2563311c69909c16d7cfb471ab7f7a)
 - [React.createElement - style](https://codepen.io/alyra/pen/JjXJqPG) | [solution](https://codepen.io/alyra/pen/848f5e1deae270f6ba3c60cf71546f3a)
