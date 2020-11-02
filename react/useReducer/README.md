# `useReducer` hook

Le hook `useReducer` permet de gérer le *state*, il a le même rôle que `useState`. 

`useState` sera le premier choix en ce qui concerne la gestion du state et `useReducer` est son alternative, plus complèxe. En fait `useReducer` et une extension de `useState`.

Pour comprendre son comportement nous allons transformer quelques exemples où nous utilisons initiallement `useState` vers `useReducer`. 

## Anatomie

```javascript
const reducer = (state, action) => { /* ... */ }

const [state, dispatch] = React.useReducer(reducer, initialState, init)
```


Comme dans l'API de `useState`, `useReducer` retourne un array, le premier élément est notre state, le deuxième une fonction (`dispatch`). La fonction `dispatch` ne modifie pas `state` directement mais délégue ça à la fonction `reducer`. Nous appellons la fonction `dispatch` à chaque fois que nous allons mettre à jour `state`, et c'est la logique de la fonction `reducer` qui met à jour state. 

```javascript
dispatch(action) 
// --->
reducer(state, action)
```

La dénomination `dispatch, action, reducer` est tout à fait facultative et suit une certaine convention qui a ces racines dans `Redux`. 

Dans notre premier exemple, pour plus de clarté, nous n'allons pas utiliser les noms `dispatch` ou `action`.

## Exemple 1

```javascript
// avec useState
const Counter = () => {
  const [count, setCount] = React.useState(0)
  const handleButtonClick = () => {
    setCount(count + 1)
  }
  return <button type="button" onClick={handleButtonClick}>{count}</button>
}
```


```javascript
// avec useReducer
const reducer = (count, newCount) => newCount
const Counter = () => {
  const [count, setCount] = React.useReducer(reducer, 0)
  const handleButtonClick = () => {
    // setCount(count) déclanche appel de reducer(count, count + 1)
    setCount(count + 1)
  }
  return <button type="button" onClick={handleButtonClick}>{count}</button>
}
```

Ce qu'on peur voir dans l'exemple ci-dessus est que la mise en place de

```javascript
const [state, setState] = React.useState(initialState)
```

et équivalent à 

```javascript
const reducer = (state, newState) => newState
const [state, setState] = React.useReducer(reducer, initialState)
```

Pour être plus précise il faudrait prendre en compte aussi que `setState` pour avoir une fonction comme paramètre, par exemple `setCount(count => count + 1)`, 

```javascript
const reducer = (state, newState) => typeof newState === 'function' ? newState(state) : newState
const [state, setState] = React.useReducer(reducer, initialState)
```

Pour résumer, `useReducer` est comme `useState` avec un paremètre de plus, la fonction `reducer` que nous pouvons tailler selon nos besoin. Par conséquant, nous avons aussi plus de liberté  en ce qui concerne comment nous utilisons la fonction `dispatch` (`setState`).

Est-ce exemple 1 plus simple (lisible, maintenable) avec `useReducer` qu'avec `useState` ? Non, nous allons pas utiliser `useReducer` dans ce type des cas.


## Exemple 2

https://codepen.io/alyra/pen/vYKjmvg

```javascript
  const [text, setText] = React.useState(
    "Portez ce vieux whisky au juge blond qui fume !? 0123456789"
  );
  const [size, setSize] = React.useState("20");
  const [italic, setItalic] = React.useState(false);
```

ou nous utilisons ensuite `setText(event.target.value)`, `setSize(event.target.value)` et `setItalic(event.target.checked)`

Voici la possible version avec `React.useReducer`

```javascript
const [state, setState] = React.useReducer( reducer, {
  text: "Portez ce vieux whisky au juge blond qui fume !? 0123456789",
  size: "20",
  italic: false
)}
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

https://codepen.io/alyra/pen/OJXZgJQ

## Exemple 3

https://codepen.io/alyra/pen/jOqYggy

```javascript
const ShoppingApp = () => {
  const [shopping, setShopping] = React.useState(["cumin", "curry", "poivre"]);
  const handleDoneClick = (product) => {
    setShopping(shopping.filter((el) => el !== product))
  };
  return (
    <section>
      <h2>My shopping List</h2>
      <ol>
        {shopping.map((product) => {
          return (
            <li key={product}>
              {product}
              <button
                onClick={() => handleDoneClick(product)}
              >
                done!
              </button>
            </li>
          );
        })}
      </ol>
      <AddProductForm shopping={shopping} setShopping={setShopping} />
    </section>
  )
}

const AddProductForm = (props) => {
  const { shopping, setShopping } = props;
  const handleFormSubmit = (event) => {
    event.preventDefault();
    const newProduct = event.target.elements.product.value;
    if (shopping.includes(newProduct)) {
      alert(`${newProduct} est déjà sur la liste`);
    } else {
      setShopping([...shopping, newProduct]);
    }
    event.target.reset();
  }
  return (
    <form onSubmit={handleFormSubmit}>
      <label htmlFor="product">
        Ajouter sur la liste
      </label>
      <input id="product" required />
    <button type="submit">
      J'ajoute !
    </button>
    </form>
  );
}
```

Dans l'exemple si-dessus nous appellons `setShopping` pour effecture une des deuz actions :
- ajouter produit sur la liste (nous pouvons appeler cette action "ADD")
- retirer produit de la li ("REMOVE")

https://codepen.io/alyra/pen/jOrxZov


Voici comment nous allons remplacer `useState`

```javascript
// avant : const [shopping, setShopping] = React.useState(["cumin", "curry", "poivre"]);
const [shopping, dispatch] = React.usereducer(shoppingReducer, ["cumin", "curry", "poivre"])
```

Et voici la fonction `shoppingReducer` :

```javascript
const shoppingReducer = (shopping, action) => {
  switch (action.type) {
    case "ADD":
      return [...shopping, action.product];
    case "REMOVE":
      return shopping.filter((el) => el !== action.product);
    default:
      throw new Error(`Unsupported action type ${action.type}`);
  }
}
```

Et nous allons utiliser `dispatch` comme ceci :

```javascript
// avant setShopping(shopping.filter((el) => el !== product))
dispatch({type: "REMOVE", product})
// avant setShopping([...shopping, newProduct])
dispatch({type: "ADD", product: newProduct})
```

## Exemple 4

`useState`
https://codepen.io/alyra/pen/VwaBvqZ

`useReducer`
https://codepen.io/alyra/pen/GRqdxrQ






