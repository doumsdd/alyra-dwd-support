# `useReducer` hook

Le hook `useReducer` permet de gérer le _state_, il a le même rôle que `useState`.

`useState` sera le premier choix en ce qui concerne la gestion du state et `useReducer` est son alternative, plus complèxe. Nous pouvons dire que `useReducer` et une extension de `useState.`

Pour comprendre son comportement nous allons transformer quelques exemples où nous utilisons initiallement `useState` vers `useReducer`.

## Anatomie

```javascript
const reducer = (state, action) => {
  /* ... */
  // retourne nouvelle valeur de state
}

const [state, dispatch] = React.useReducer(reducer, initialState, init)
```

Comme dans l'API de `useState`, `useReducer` retourne un array, le premier élément est notre state, le deuxième une fonction (`dispatch`).

Nous appellons la fonction `dispatch` à chaque fois où nous allons mettre à jour `state`.Pourtant la fonction `dispatch` ne modifie pas `state` directement. Elle délègue ceci à la fonction `reducer`.

La fonction `reducer` retourne une nouvelle valeur de state et si la modification de state est détéctée le re-render est déclanché.

```javascript
dispatch(action)
// --->
reducer(state, action)
```

![](https://wptemplates.pehaa.com/assets/alyra/usereducer-anatomie.png)

La dénomination `dispatch`, `action` et `reducer` est tout à fait facultative et suit une certaine convention qui a ces racines dans `Redux`.

Dans notre premier exemple, pour voir plus clairement le passage de `useState` vers `useReducer` nous n'allons pas utiliser les noms `dispatch` ou `action`.

## Exemple 1

```javascript
// avec useState
const Counter = () => {
  const [count, setCount] = React.useState(0)
  const handleButtonClick = () => {
    setCount(count + 1)
  }
  return (
    <button type="button" onClick={handleButtonClick}>
      {count}
    </button>
  )
}
```

```javascript
// avec useReducer
const reducer = (count, newCount) => newCount
const Counter = () => {
  const [count, setCount] = React.useReducer(reducer, 0)
  const handleButtonClick = () => {
    setCount(count + 1)
    // setCount(count + 1) délègue et appelle reducer(count, count + 1)
  }
  return (
    <button type="button" onClick={handleButtonClick}>
      {count}
    </button>
  )
}
```

Ce qu'on peut voir dans l'exemple ci-dessus est que la mise en place de

```javascript
const [state, setState] = React.useState(initialState)
```

et équivalent à

```javascript
const reducer = (state, newState) => newState
const [state, setState] = React.useReducer(reducer, initialState)
```

où nous ajoutons un étape supplémentaire - `reducer`.

---

**Digression (optionnelle) :** Pour être plus précis, il faudrait prendre en compte aussi que `setState` peut avoir une _fonction_ comme paramètre, par exemple `setCount(count => count + 1)`. Le code ci-dessous fonctionne correctement dans les 2 cas `setCount(count + 1)` et `setCount(count => count + 1)` :

```javascript
const reducer = (state, newState) =>
  typeof newState === "function" ? newState(state) : newState
const [state, setState] = React.useReducer(reducer, initialState)
```

---

Pour résumer, `useReducer` est comme `useState` avec un étape supplémentaire, la fonction `reducer` que nous pouvons tailler selon nos besoin. Par conséquant, nous avons aussi plus de liberté en ce qui concerne l'utilisation de la fonction `dispatch` (ou `setState`).

Est-ce exemple 1 plus simple (lisible, maintenable) avec `useReducer` qu'avec `useState` ? Non, nous allons pas utiliser `useReducer` dans ce type des cas.

## Exemple 2

https://codepen.io/alyra/pen/vYKjmvg

```javascript
const [text, setText] = React.useState(
  "Portez ce vieux whisky au juge blond qui fume !? 0123456789"
)
const [size, setSize] = React.useState("20")
const [italic, setItalic] = React.useState(false)
```

ou nous utilisons ensuite

- `setText(event.target.value)`,
- `setSize(event.target.value)`
- `setItalic(event.target.checked)`

Voici la possible version avec `React.useReducer`

```javascript
const initialState = {
  text: "Portez ce vieux whisky au juge blond qui fume !? 0123456789",
  size: "20",
  italic: false,
}
const [state, setState] = React.useReducer(reducer, initialState)
```

avec `reducer` défini comme ci-dessous :

```
const reducer = (state, newState) => {
  return {
    ...state,
    ...newState
  }
}
```

et les mise à jour de state appelées comme ceci :

- `setState({ text: event.target.value })`,
- `setState({ size: e.target.value })`
- `setState({ italic: e.target.checked })`

Vous trouverez le code complet dans le pen suivant :

https://codepen.io/alyra/pen/OJXZgJQ

## Exemple 3

https://codepen.io/alyra/pen/jOqYggy

```javascript
const ShoppingApp = () => {
  const [shopping, setShopping] = React.useState(["cumin", "curry", "poivre"])
  const handleDoneClick = (product) => {
    setShopping(shopping.filter((el) => el !== product))
  }
  return (
    <section>
      <h2>My shopping List</h2>
      <ol>
        {shopping.map((product) => {
          return (
            <li key={product}>
              {product}
              <button onClick={() => handleDoneClick(product)}>done!</button>
            </li>
          )
        })}
      </ol>
      <AddProductForm shopping={shopping} setShopping={setShopping} />
    </section>
  )
}

const AddProductForm = (props) => {
  const { shopping, setShopping } = props
  const handleFormSubmit = (event) => {
    event.preventDefault()
    const newProduct = event.target.elements.product.value
    if (shopping.includes(newProduct)) {
      alert(`${newProduct} est déjà sur la liste`)
    } else {
      setShopping([...shopping, newProduct])
    }
    event.target.reset()
  }
  return (
    <form onSubmit={handleFormSubmit}>
      <label htmlFor="product">Ajouter sur la liste</label>
      <input id="product" required />
      <button type="submit">J'ajoute !</button>
    </form>
  )
}
```

Dans l'exemple si-dessus nous appellons `setShopping` pour effectuer une des deux actions :

- ajouter un nouvel produit sur la liste (nous pouvons appeler cette action "ADD")
- retirer un produit de la liste ("REMOVE")

Par convention les noms des actions sont souvent en majuscules.

https://codepen.io/alyra/pen/jOrxZov

Voici comment nous allons remplacer `useState` :

```javascript
// avant : const [shopping, setShopping] = React.useState(["cumin", "curry", "poivre"]);
const [shopping, dispatch] = React.useReducer(shoppingReducer, [
  "cumin",
  "curry",
  "poivre",
])
```

Et voici la fonction `shoppingReducer` :

```javascript
const shoppingReducer = (shopping, action) => {
  switch (action.type) {
    case "ADD":
      return [...shopping, action.product]
    case "REMOVE":
      return shopping.filter((el) => el !== action.product)
    default:
      throw new Error(`Unsupported action type ${action.type}`)
  }
}
```

Quand la fonction `dispatch` est appellée, `shoppingReducer` est executée. Les arguments de `shoppingReducer` est state (`shopping`) dans notre cas, 2e paramètre (`action`) reprend l'argument passé à `dispatch`.

Nous devons alors passer `type` et `product` dans `dispatch`.

```javascript
// avant setShopping(shopping.filter((el) => el !== product))
dispatch({ type: "REMOVE", product })
// avant setShopping([...shopping, newProduct])
dispatch({ type: "ADD", product: newProduct })
```

Vous trouverez le code complet ici :

https://codepen.io/alyra/pen/jOrxZov

## Exemple 4

`useState`
https://codepen.io/alyra/pen/VwaBvqZ

`useReducer`
https://codepen.io/alyra/pen/GRqdxrQ
