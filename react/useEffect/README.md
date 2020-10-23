# Side effect & React useEffect() hook

## Side effects (effets bord)

La mission d'un component React et de créer un rendu dans la page. La fonction qui définit le component est reévaluée à chaque fois où une valeur de props ou la valeur de state change.

Le nouvel rendu est généré, il est comparé détail par détail avec le rendu existant. Les éléments qui changent, sont mis à jour.

Parfois, nous avons besoin pour faire quelque chose d'autre, par exemple :

- enregistrer une variable de state dans l'objet `localStorage`,
- effectuer une rêquete HTTP,
- modifier le `document`, en dehors de notre component ou même toute notre application (en dehors de notre `div#root`), par exemple `document.title`
- mettre en place `setTimeout` ou `setInterval`
- ajouter un eventListener à l'objet `window`
  ...

Ce sont tous des exemples de _side effects_

Autrement dit, _side effects_ concernent ce qui est en dehors du _scope_ de notre component.

Pour mettre en place les _side effects_, React nous met en disposition un hook `useEffect`.

## anatomie

![](https://assets.codepen.io/4515922/useEffectAnatomy.png)

### à chaque render (par défaut)

```javascript
useEffect(() => {
  console.log("je viens de render (ou (re-render))")
})
```

[[[pen slug-hash='gOrzKyO' height='300' theme-id='1']]]

### au montage (_mount_, initial render)

```javascript
useEffect(() => {
  console.log("je viens de monter!!!")
}, [])
```

Ex. 1

[[[pen slug-hash='PoNeaMq' height='300' theme-id='1']]]

Ex. 2

[[[pen slug-hash='jOqxKjB' height='300' theme-id='1']]]

### quand state ou props change

```javascript
useEffect(() => {
  console.log('myVar1 vient d'être modifiée', myVar1)
}, [myVar1])
```

### avec nettoyage

```javascript
React.useEffect(() => {
  console.log("mount")
  return () => {
    console.log("cleanup on unmount")
  }
}, [])
```

```javascript
React.useEffect(() => {
  console.log("render")
  return () => {
    console.log("cleanup before re-render")
  }
})
```

[[[pen slug-hash='BaKxxpx' height='300' theme-id='1']]]

---

## Exercices :

[Todos App - localStorage et compagnie](https://github.com/pehaa/alyra-todos-localstorage)
