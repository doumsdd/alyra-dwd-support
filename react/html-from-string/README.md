# Rendering _HTML from string_ dans React

Souvent le contenu que nous affichons avec React provient d'une source tiers (api, base de données). Nous les récupperons en tant qu'un objet, par exemple :

```javascript
const alyra = {
  name: "Alyra",
  link: "https://alyra.fr",
  description: `<p>Une école <strong>au coeur de la blockchain.</strong> Fondée par des passionés et ouverte à toutes et tous.</p>`,
}
```

Dans ce cas là, `name`, `link`, `description` sont en format `string`. Le clés `description` contiennent les balises HTML. Insérer des balises HTML d'une source tiers est une opération à risque, exposant notre application aux attaques XSS. Pour nous protéger contre ceci, React échappe toutes les balises HTML. Regardons ce que ça veut dire en pratique.

```javascript
const School = (props) => {
  const { name, children } = props
  return (
    <article className="p-3 mb-3 border shadow">
      <h2 className="text-center">{name}</h2>
      {children}
    </article>
  )
}

const App = () => {
  return <School name={alyra.name}>{alyra.description}</School>
}

ReactDOM.render(<App />, document.getElementById("root"))
```

![](https://assets.codepen.io/4515922/alyrahtmlstring.png)

Voici notre **problème** : Description est recupérée depuis le string dans `alyra.description`. Pour des raisons de sécurité toutes les balises sont converties en string.

```javascript
const htmlString = `<h1>Je suis un string <b>avec HTML !</b></h1>`
const App = () => <div>{htmlString}</div>
```

![](https://assets.codepen.io/4515922/htmlstring.png)

## Solution (1) - dangerouslySetInnerHTML

Afin de rendre le string en format HTML, nous pouvons utiliser l'attribut `dangerouslySetInnerHTML`.  
Nous pouvons comparer `dangerouslySetInnerHTML` à `innerHTML` dans le DOM.

```javascript
const htmlString = `<h1>Je suis un string <b>avec HTML !</b></h1>`

const App = () => <div dangerouslySetInnerHTML={{ __html: htmlString }} />
```

`dangerouslySetInnerHTML` est une props React, que nous pouvons utiliser avec des balises de DOM (mais pas avec des components ou `React.Fragment`).  
La valeur de `dangerouslySetInnerHTML` doit être un objet avec une clé `__html`.

```javascript
const alyra = {
  name: "Alyra",
  description: `<p>Une école <strong>au coeur de la blockchain.</strong> Fondée par des passionés et ouverte à toutes et tous.</p>`,
}

const School = (props) => {
  const { name, children } = props
  return (
    <article className="p-3 mb-3 border shadow">
      <h2 className="text-center">{name}</h2>
      <div dangerouslySetInnerHTML={{ __html: children }} />
    </article>
  )
}

const App = () => {
  return <School name={alyra.name}>{alyra.description}</School>
}

ReactDOM.render(<App />, document.getElementById("root"))
```

https://codepen.io/alyra/pen/WNwXNmv

## Solution (1a) - dangerouslySetInnerHTML + DOMPurify

Sanitized avec [DOMPurify](https://github.com/cure53/DOMPurify)

https://codepen.io/alyra/pen/ZEWjbQy

## html-react-parser

Il est aussi possible d'utiliser une bibliothèque externe, par exemple [`html-react-parser`](https://github.com/remarkablemark/html-react-parser)

```html
<div id="root"></div>
<script src="https://unpkg.com/react/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/html-react-parser@latest/dist/html-react-parser.min.js"></script>
```

```javascript
const alyra = {
  name: "Alyra",
  description: `<p>Une école <strong>au coeur de la blockchain.</strong> Fondée par des passionés et ouverte à toutes et tous.</p>`,
}

const School = (props) => {
  const { name, children } = props
  return (
    <article className="p-3 mb-3 border shadow">
      <h2 className="text-center">{name}</h2>
      {children}
    </article>
  )
}

const App = () => {
  return <School name={alyra.name}>{HTMLReactParser(alyra.description)}</School>
}

ReactDOM.render(<App />, document.getElementById("root"))
```

[[[pen slug-hash='dyMZPdE' height='300' theme-id='1']]]

Sanitized avec [DOMPurify](https://github.com/cure53/DOMPurify)

[[[pen slug-hash='gOrjaMY' height='300' theme-id='1']]]
