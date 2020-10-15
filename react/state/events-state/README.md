
# Handling Events &  💫 State 💫

## Handling Events

Comment intégrer la gestion des événements (click, change, input, etc.) avec JSX.

```javascript
const Button = () => {
  return (<button onClick={() => alert('Hello')}>Click me</button>
}
```

```javascript
const Input = () => {
  const handleNameChange = (event) => {
    alert(`Hello ${event.target.value}`)
  }
  return (
    <input onChange={handleNameChange} placeholder="Votre nom"/>
  )
}
```

**À retenir :**

- Les événements de React sont nommés en camelCase : onClick, onChange, onSubmit, onKeyUp,...
- En JSX on passe une fonction event handler (géstionnaire d’événements)  

```javascript
onClick={(event) => {...}}
```

```javascript
onClick={handleButtonClick}
```

```javascript
onSubmit={handleLoginSubmit}
```

```javascript
// si on a besoin de passer un argument (ex. id) dans event handler
onClick={(event) => handleButtonClick(id, event)}
```

- La fonction event handler a accès à l'objet `event`
- `event.target` correspond à l'élément auquel event handler est acroché. En particulier, on utilise souvent `event.target.value`

[[[pen slug-hash='ZEWvjQN' height='300' theme-id='1']]]


## Component interactif (approche "from scratch")

Dans React, *state* variable est une variable qui est responsable pour éventuel re-render d'un component. Si une des variables de *state* change, le component React se met à jour.

Le code ci-dessous illustre comment ceci fonctionne sous le capot :

```javascript
// notre component App a 2 state variables
const state = { 
  like: false, 
  name: "Unconnu",
}

const setLike = (value) => {
  if (state.like !== value) {
    state.like = value;
    renderFunction();
  }
}

const setName = (value) => {
  if (state.name !== value) {
    state.name = value;
    renderFunction();
  }
}

const App = () => {
  const { like, name } = state

  const handleLikeChange = () => {
    setLike(event.target.checked)
  }
  
  const handleNameChange = (event) => {
    setName(event.target.value)
  }
  
  return (
    <div>
      <input onChange={handleNameChange} />
      <input type="checkbox" onChange={handleLikeChange} />
      <p>
        {name} dit : "{like ? `j'aime React` : `je n'aime pas React`}".
      </p>
    </div>
  );
};
// nous définissons une fonction pour effectuer render
function renderFunction() {
  ReactDOM.render(<App />, document.getElementById("root"))
}
// render initiale
renderFunction()
```

[[[pen slug-hash='VwamzdG' height='300' theme-id='1']]]

Pour la première fois, nous avons un component interactif.
Nous allons maintenant utiliser la fonction React useState, qui prendra en charge la géstion du re-render.

## React.useState hook

On appelle `React.useState` avec la valeur initiale de la variable state.
`React.useState` **retourne un array,** son première élément est une clé de state variable, le 2e la fonction pour modifier la valeur de notre state variable. 

```javascript
const App = () => {
  const [like, setLike] = React.useState(false)
  const [name, setName] = React.useState('Unconnu')

  const handleLikeChange = (event) => {
    setLike(event.target.checked)
  }
  
  const handleNameChange = (event) => {
    setName(event.target.value)
  }
  
  return (
    <div>
      <input onChange={handleNameChange} />
      <input type="checkbox" onChange={handleLikeChange} />
      <p>
        {name} dit : "{like ? `j'aime React` : `je n'aime pas React`}".
      </p>
    </div>
  );
};
// nous nous précoccupons uniquement de render initial
ReactDOM.render(<App />, document.getElementById("root"))
```

[[[pen slug-hash='xxVRPYw' height='300' theme-id='1']]]

### Simple Counter
[[[pen slug-hash='NWNXBdL' height='300' theme-id='1']]]

### Alyra Gradients - header interactif
[[[pen slug-hash='rNepaOy' height='300' theme-id='1']]]

## Class Components

React hooks, en particulier `useState` ne marchent pas dans les class components.

Dans ce cas là, nous initialisons `state` dans le constructeur, et utilisant fonction `setState` pour les mises à jour de state.

```javascript
class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      like: true,
      name: 'Unconnu'
    }
  }
  handleLikeChange(event) {
    this.setState({ like: event.target.checked });
  }
  handleNameChange(event) {
    this.setState({ name: event.target.value });
  }
  render() {
    <div>
      <input onChange={() => this.handleNameChange()} />
      <input
        type="checkbox" 
        onChange={(event) => this.handleLikeChange(event)}
      />
      <p>
        {this.state.name} dit : "{this.state.like ? `j'aime React` : `je n'aime pas React`}".
      </p>
    </div>
  }
}
```

[[[pen slug-hash='ZEWBvEG' height='300' theme-id='1']]]

---

## Exercices :

 - [Events - select change](https://codepen.io/alyra/pen/zYqzxgv) | [solution](https://codepen.io/alyra/pen/5a51da89910b5b8aa9e33e55e64450c2)
 - [Events - select change](https://codepen.io/alyra/pen/oNxwXWG) | [solution](https://codepen.io/alyra/pen/683f280874ff466121c5115dd0d20943)
 - [State - Fix me - click count](https://codepen.io/alyra/pen/jOqYOQN) | [solution](https://codepen.io/alyra/pen/5f1330ce589c02ee762400ee9579e427)
 - [Clicks countdown](https://codepen.io/alyra/pen/GRZyWxb) | [solution](https://codepen.io/alyra/pen/19bc3ca167473f4a385088681fcd4011)
 - [Clicks compteurs](https://codepen.io/alyra/pen/NWNXper) | [solution](https://codepen.io/alyra/pen/4039761b2dceb4365b22730e69e9de04)
 - [Dark Mode](https://codepen.io/alyra/pen/OJNzPgL) | [solution](https://codepen.io/alyra/pen/4cab28e7eab6f5a480df16bb73f12e95)
 - [State - en lire plus](https://codepen.io/alyra/pen/KKzNoNx) | [solution](https://codepen.io/alyra/pen/ac7586841147fe68381f340d7dc2d46b)