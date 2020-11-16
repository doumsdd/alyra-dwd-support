# Objects - introduction

Un objet est un ensemble de propriétés regroupées dans une structure clé-valeur. Par exemple le droid R2-D2 a plusieurs propriétés :
- nom, 
- taille, 
- poids,
- couleur des yeux.

L'objet `rdd2` aura alors les clés : `name`, `height`, `mass` et `eyeColor`. Leur valeurs respectives sont : `"R2-D2"`, `96`, `32` et `"red"`. Ainsi nous regroupons toutes les informations concernant R2-D2 dans un objet `rdd2`.

```javascript
const rdd2 = {
  name: "R2-D2",
  height: 96,
  mass: 32,
  eyeColor: "red",
}
```

Voici un autre exemple :

```javascript
const paulina = {
  name: "Paulina",
  position: "formateur",
  timeBasis: "plein temps",
  mission: ["cours HTML", "cours CSS", "cours JS", "cours React"],
}
```

On peut combiner arrays et objets, par exemple :

```javascript
const veilles = [
  {
    subject: "Ethers.Js",
    date: "29/07/2020",
    category: "Dev BC",
  },
  {
    subject: "Smart Contract",
    date: "30/07/2020",
    category: "Blockchain",
  },
  {
    subject: "Licence MIT",
    date: "31/07/2020",
    category: "DEV",
  },
  {
    subject: "Snippets",
    date: "03/08/2020",
    category: "DEV",
  },
]
```

Ici, `veilles` est un array contenant des objets. Dans la variable `paulina`, la clé mission contient un array des strings.

## Création

```javascript
const obj1 = {} // Object {}
const obj2 = new Object() // Object {}
const obj3 = {
  key1: value1,
  key2: value2,
}
```

Comme pour les arrays (qui sont aussi de type `"object"`), des variables stockent des références et pas les object eux-mêmes.

Par conséquence :

```javascript
const obj1 = {}
const obj2 = {}
obj1 === obj2 // false
```

## Modification

```javascript
const planningVacancesPaulina = {
  destination: "Ile de Batz",
  start: "2020/08/15",
  transport: "train",
  shopping: ["2 t-shirt", "lunettes", "crème spf50"],
}

const planningVacancesVains = planningVacancesPaulina
// modification
planningVacancesVains.start = "2020/08/14"
// ajout d'une nouvelle clé
planningVacancesVains.end = "2020/08/30"
```

On peut aussi **supprimer une clé** :

```
delete planningVacancesPaulina.transport
```

Afin d'accéder une clé :

```javascript
console.log(planningVacancesPaulina.destination)
console.log(planningVacancesPaulina["destination"])
console.log(planningVacancesPaulina.shopping[1])
```

Et si la valeur de notre clé est stockée dans une variable :

```javascript
const key = "end"
console.log(planningVacancesPaulina[key])
```

## Parcourir l'objet

```javascript
const droid = {
  name: "R2-D2",
  height: 96,
  mass: 32,
  eyeColor: "red",
}
```

Nous pouvons lister (ceci dit le résultat sera un array) les clés avec la méthode `Object.keys()` : 

```javascript
// les clés
Object.keys(droid) // ['name', 'height', 'mass', 'eyeColor']
```

De la même façon, nous pouvons lister les valeurs avec la méthode `Object.values()` : 

```javascript
// les valeurs
Object.values(droid) // ['R2-D2', 96, 32, 'red']
```

Et finalement, nous pouvons lister (format array) les pairs clé-valeur avec la méthode `Object.entries()` : 

```javascript
// les pairs clé, valeur
Object.entries(droid) // [['name', 'R2-D2'], ['height', 96], ['mass', 32], ['eyeColor', 'red']]
```

Afin de parcourir l'objet par les clés, nous avons dans notre arseanl la boucle `for in` (attention, pour des arrays c'était `for of`)

```javascript
for (let key in droid) {
  console.log(key, droid[key])
}
```

Etant donné que les méthodes `Object.keys`, `Object.values` et `Object.entries` retournent des arrays, on peut "les marier" avec  des méthodes telles que `map`, `filter`, `find`, etc., ainsi que la loop `for of`.

```javascript
for (let value of Object.values(droid)) {
  console.log(value)
}
```

```javascript
// filtrer toutes les valeur de type number
Object.values(character).filter((el) => typeof el === "number")
```

## Vérifier si une clé existe

```javascript
const droid = {
  name: "R2-D2",
  height: 96,
  mass: 32,
  eyeColor: "red",
}

console.log("eyeColor" in droid)
console.log(droid.eyeColor !== undefined)
console.log(typeof droid.eyeColor !== "undefined")
```

## Merge objects

```javascript
const myInfo = {
  firstName: "Paulina",
  lastName: "Hetman",
  contrat: "freelance",
}

const professionalInfo = {
  firstName: "Paulina",
  lastName: "Hetman",
  school: "Alyra",
  position: "formateur",
  contrat: "cdd",
}

Object.assign(myInfo, professionalInfo)
console.log(myInfo)
console.log(Object.assign(myInfo, professionalInfo))
/*
Object {
  contrat: "cdd",
  firstName: "Paulina",
  lastName: "Hetman",
  position: "formateur",
  school: "Alyra"
}
*/
```

`Object.assign(object1, object2, object3)` merge les 3 objets, si une clé est dupliquée, c'est l'objet à droite qui emporte celui à gauche

Cette méthode modifie `object1`.

https://codepen.io/alyra/pen/abNyKYZ

On peut aussi "merger" des objets sans modifier l'objet d'entrée :

```javascript
const newObject1 = { {...myInfo}, professionalInfo }
```

https://codepen.io/alyra/pen/abNyKKm

---

Exercices

- [js quizzes - objects](https://javascript-quizzes.netlify.app/objects)
- [Objects - users](https://codepen.io/alyra/pen/eYJyLVO) | [solution](https://codepen.io/alyra/pen/8ad56700fd9e9113ff24b255810110e8)
- [Objects - salaires](https://codepen.io/alyra/pen/qBbpKxY) | [solution](https://codepen.io/alyra/pen/c16eda6bac531e22021319550cd176d5)
- [Objects - gradients](https://codepen.io/alyra/pen/wvMNgzG) | [solution](https://codepen.io/alyra/pen/4937a3f2174d6efa0ca82609cadbb893)
