# Destructuring Assignement

(fr. Affectation par décomposition)

## objects

```javascript
const name = 'Deej'
const age = 300
const alien = {
  name,
  age
}
/* équivalent à
alien = {
  name (clé "name"): name (valeur de la variable name)
  age (clé "age"): age (valeur de la variable age)
}
```

Ca marche aussi dand le "sens inverse" :

```javascript
const alien = {
  name: "Deej",
  age: 300,
}
const { name } = alien
// variable name égale à 'Deej'
const { age } = alien
// variable age égale à 300
```

Définir plusieures variables à la fois est aussi possible est souvent utilisé :

```javascript
const alien = {
  name: "Deej",
  age: 300,
}
const { age, name } = alien
// variable name égale à 'Deej'
// variable age égale à 300
```

S'il n'y a pas de clé correspandant au nom de la variable :

```javascript
const alien = {
  name: "Deej",
  age: 300,
}

const { age, id, name } = alien
// variable age égale à 300
// variable id égale à undefined
// variable name égale à 'Deej'
```

On peut aussi avoir des valeur par défaut :

```javascript
const alien = {
  name: "Deej",
  id: "_deej",
}

const { age = 100, id, name } = alien
// variable age égale à 100
// variable id égale à '_deej'
// variable name égale à 'Deej'
```

On peut aussi récuperer une partie qui "reste" d'objet dans une variable, souvent on utilisera le nom `rest` pour cette variable (ceci est une convention). Pour cela on utilise les "..."

```javascript
const alien = {
  name: "Deej",
  id: "_deej",
  age: 200,
}

const { name, ...rest } = alien
console.log(name) // 'Deej'
console.log(rest)
/*
{
  age: 200,
  id: "_deej"
}
*/
```

## arrays

Dans arrays les valeurs sont indéxées et ne possèdent pas des noms des clés mais la décomposition est possible :

```javascript
const spices = ["chili", "poivre", "sel"]
const [a, b] = spices
// a - premier élément de l'array spices -> 'chili'
// b - 2e élément de l'array spices -> 'poivre'
```

```javascript
const spices = ["chili", "poivre", "sel"]
const [a, , b] = spices
// a - premier élément de l'array spices -> 'chili'
// b - 3e élément de l'array spices -> 'sel'
```

```javascript
const spices = ["chili", "poivre", "sel"]
const [a, ...rest] = spices
// a - premier élément de l'array spices -> 'chili'
// rest - ['poivre', 'sel']
```

```javascript
const spices = ["chili", "poivre", "sel"]
const [a, b, c, d] = spices
// a - premier élément de l'array spices -> 'chili'
// b - 2e élément de l'array spices -> 'poivre'
// c - 3e élément de l'array spices -> 'sel'
// d - 4e élément de l'array spices -> undefined
```

---

## Exercices :

[js quizzes - destructuring](https://javascript-quizzes.netlify.app/destructure)
