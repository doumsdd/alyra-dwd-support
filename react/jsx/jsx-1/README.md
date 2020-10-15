# JSX - 1

Posez-vous des questions, mais en quoi, `React.createElement` nous facilite la vie,... on dirait le contraire... ? Je pense que c'est un reflèxe tout à fait légitime. Créer les structures plus complèxe demande beaucoup de code, et le tout n'est pas forcement très lisible. 

Heureusement, **JSX** nous vient à la rescousse !

JSX est une extension syntaxique de JavaScript, créée par des dévelopeurs de React et recommandé par React. 

C'est un peu comme si on écrivait du HTML directement dans JavaScript.

Avec JSX nous passons de (avant) :

```javascript
const element = React.createElement(
  "h1",
  {lang: "en"},
  "Hello World!"
)
```

vers :

```javascript
const element = <h1 lang="en">Hello World!</h1>
```

ou :

```javascript
const element = React.createElement(
  "article",
  {
    className: "card"
  }
  React.createElement("h2", null, "Secrets des pandas roux") 
  React.createElement("img", {src: "panda-roux.png", alt: "Panda roux dort sur une branche."})
  React.createElement("p", null, "Le petit panda est un carnivore, qui ne mange jamais de la viande...")
)
```

vers (après) :

```javascript
const element = (
  <article className="card">
    <h2>Secrets des pandas roux</h2>
    <img src="panda-roux.png" alt="Panda roux dort sur une branche." />
    <p>Le petit panda est un carnivore, qui ne mange jamais de la viande...</p>
  </article>
)
```

## babel

Vous vous rappelez de sass ? nous avons dit que sass est une extension de css. Le navigateur ne comprend pas sass et le code sass doit passer par le compilateur et être transformé en css. C'est pareil pour JSX, les navigateurs ne comprennent pas cette syntaxe. Comme pour sass, nous devons utiliser un compilateur, et nous allons utiliser [**babel**](https://babeljs.io).

- [babel on-line demo](https://babeljs.io/en/repl#?browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=MYewdgzgLgBApgGzgWzmWBeGAeAFgRgD4AJRBEGAdRACcEATbAegMKA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=react&prettier=false&targets=&version=7.7.4&externalPlugins=)

- utiliser *standalone* babel et `<script type="text/babel">`

```html
<div id="root"></div>
<script src="https://unpkg.com/react/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.js"></script>
<script type="text/babel">
// javascript avec jsx vient ici
</script>
```

- babel est directement disponible dans CodePen > JS > JavaScript Preprocessors > Babel. Nous allons souvent l'utiliser avec la feuille de style de bootstrap 5 - [voici une template](https://codepen.io/pen/?template=bGpwWNB)

- configuration inclue dans les starters (on vera ça bientôt)

## toutes les balises sont obligatoirement fermées (xml-style)

Dans HTML on peut se permettre de ne pas fermer des balises auto-fermantes (self-closing tags), tel que `<input>` ou `<img src="img1.jpg" alt="">`.  

Ceci n'est pas correcte dans JSX, alors ce sera `<input />` et `<img src="img1.jpg" alt="" />`

## React.Fragment

```javascript
element = (
  <React.Fragment>
    <dt>JSX</dt>
    <dd>une extension syntaxique de JavaScript</dd>
  </React.Fragment>
)
```

ou 😍😍😍 :

```javascript
element = (
  <>
    <dt>JSX</dt>
    <dd>une extension syntaxique de JavaScript</dd>
  </>
)
```

## Commentaires

```javascript
{ /* je suis un commentaire  */ }
```

## ReactDOM

On peut utiliser JSX directement avec `ReactDOM` :

```javascript
ReactDOM.render(<h1>Hello World</h1>, root)
```

## React sans JSX

[en lire plus](https://fr.reactjs.org/docs/react-without-jsx.html)

--- 

## Exercices

 - [JSX p](https://codepen.io/alyra/pen/OJNbKMo) | [solution](https://codepen.io/alyra/pen/29e2be325c73498465349b7eb816d4b1)
 - [JSX button](https://codepen.io/alyra/pen/MWybNyY) | [solution](https://codepen.io/alyra/pen/24c0e41e939ac4cc1773c654711bf2cd)
 - [JSX h1](https://codepen.io/alyra/pen/wvGoVGR) | [solution](https://codepen.io/alyra/pen/aa7b96a373353287f147da0cf3937fb9?editors=1010)
 - [JSX - header](https://codepen.io/alyra/pen/eYZdoWg) | [solution](https://codepen.io/alyra/pen/50bee6a7d1c810dfccba46d5e4dee82b)
 - [JSX - input](https://codepen.io/alyra/pen/MWyoLrY) | [solution](https://codepen.io/alyra/pen/cf85be5c0ae3a664db66486387b908c5)
 - [JSX - label + input](https://codepen.io/alyra/pen/GRZEzyG) | [solution](https://codepen.io/alyra/pen/3b5c8b252ef90a019d3db1c8990b6677)
 - [JSX - style](https://codepen.io/alyra/pen/vYGJrLx) | [solution](https://codepen.io/alyra/pen/5882c4df35ceb675f3e246b2829bff4a)










