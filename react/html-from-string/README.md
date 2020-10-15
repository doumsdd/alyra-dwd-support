# Rendering _HTML from string_ dans React

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
  return <School name={alyra.name}>{alyra.description}</School>
}

ReactDOM.render(<App />, document.getElementById("root"))
```

![](https://assets.codepen.io/4515922/alyrahtmlstring.png)

**Problème** : Description est recupérée depuis le string dans `alyra.description`. Pour des raisons de sécurité toutes les balises sont converties en string.

```javascript
const htmlString = `<h1>Je suis un string <b>avec HTML !</b></h1>`
const App = () => <div>{htmlString}</div>
```

![](https://assets.codepen.io/4515922/htmlstring.png)

## dangerouslySetInnerHTML

Afin de rendre le string en format HTML, nous pouvons utiliser `dangerouslySetInnerHTML`.  
`dangerouslySetInnerHTML` est l’équivalent React de `innerHTML` dans le DOM.

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

[[[pen slug-hash='WNwXNmv' height='300' theme-id='1']]]

Sanitized avec [DOMPurify](https://github.com/cure53/DOMPurify)

[[[pen slug-hash='ZEWjbQy' height='300' theme-id='1']]]

## html-react-parser

Il est aussi possible d'utiliser une bibliothèque externe, par exemple [`html-react-parser`](https://github.com/remarkablemark/html-react-parser)

```html
<div id="root"></div>
<script
  crossorigin
  src="https://unpkg.com/react@16/umd/react.development.js"
></script>
<script
  crossorigin
  src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"
></script>
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
