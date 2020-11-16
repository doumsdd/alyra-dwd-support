# Arrays - bases

Arrays (tableaux) permettent de stocker des collections (listes) de données.

## Création

```javascript
const myList1 = [] // []
const myList2 = new Array() // []
const myListMisc = new Array("hello", 13, 8 === "8") 
// ['hello', 13, false]
const shopping = ["t-shirt", "shorts", "paréo"]
const myArray = new Array(3) // [undefined, undefined, undefined]
const myLetters = new Array.from("abcd") // ["a", "b", "c", "d"]
```

## Nombre d'éléments

```javascript
const myList1 = []
myList1.length // 0
const shopping = ["t-shirt", "shorts", "pareo"]
shopping.length // 3
```

La propriété `length` est souvent utilisée dans le contexte booléen, afin de vérifier si un array est vide. (Rappelons-nous que `[]` est une valeur *truthy*). Dans l'exemple suivant, nous utilisons `shopping.length` puisque `shopping` serait toujours évalué *truthy*.

```javascript
if (shopping.length) {
  alert("let's go shopping !")
} else {
  alert("Vous n'avez rien à acheter")
}
```

## Élément par index

Les éléments de la liste sont indexés à partir de zéro: 0, 1, &hellip; Le dernier élément de la liste `myList` a l'index `myList.length - 1`

```javascript
const myList1 = [2, 5, 8, 90]
myList[0] // premier élément de la liste, ici 2
myList[1] // 2e, ici 5
myList[3] // 90
myList[myList.length - 1] // myList[3] -> 90
myList[myList.length] // undefined
```

Ceci permet de lire, mais aussi de modifier la valeur

```javascript
const myList1 = [2, 5, 8, 90]
myList1[2] = -1
// [2, 5, -1, 90]
```

## Voici comment on peut ajouter et enlever les éléments

```javascript
const myList1 = [2, 5, 8, 90]
myList1.pop() // myList1 devient [2, 5, 8], retourne 90
myList1.push(77) // myList1 devient [2, 5, 8, 77], retourne 4
myList1.shift() // myList1 devient [5, 8, 77], retourne 2
myList1.unshift(-11) // myList1 devient [-11, 5, 8, 77], retourne 4
```
### `push` & `unshift`

Méthodes `push` et `unshift` modifient l'array et retournent la longueur (`length`) de l'array  après modification

```javascript
const myList1 = [2, 5, 8, 90]
let newLength = myList1.push(80) // myList1 devient [2, 5, 8, 90, 80]
console.log(newLength) // 5
```

### `pop` & `shift`

Méthodes `pop` et `shift` modifient l'array et retournent l'élément enlevé.

```javascript
const myList1 = [2, 5, 8, 90]
const removed = myList1.pop() // myList1 devient [2, 5, 8]
console.log(removed) // 90
```

Attention : Les méthodes `pop` et `push` sont beaucoup plus rapide qut `shift` et `unshift`.

Les méthodes `pop`, `push` et `shift`, `unshift` opèrent sur les extrémités d'un array. Nous avons aussi une méthode générique `splice`

### `splice`

La syntaxe: `arr.splice(index[, deleteCount, elem1, ..., elemN])` peut être lu :

- positionne-toi au numéro indiqué par index, enlève `deleteCount` éléments et insère `elem1, ..., elemN`

Méthode `splice` modifie `arr` et retourne l'array des éléments enlevés.

Voici les exemples (source [splice sur mdn](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/splice))

```javascript
const mesPoissons = ["scalaire", "clown", "mandarin", "chirurgien"]

// supprime 0 élément à partir de l'index 2, et insère "tambour"
let enleves = mesPoissons.splice(2, 0, "tambour")
// mesPoissons est ["scalaire", "clown", "tambour", "mandarin", "chirurgien"]
// enleves est [], aucun élément supprimé

// supprime 1 élément à partir de l'index 3
enleves = mesPoissons.splice(3, 1)
// mesPoissons est ["scalaire", "clown", "tambour", "chirurgien"]
// enleves est ["mandarin"]

// supprime 1 élément à partir de l'index 2, et insère "trompette"
enleves = mesPoissons.splice(2, 1, "trompette")
// mesPoissons est ["scalaire", "clown", "trompette", "chirurgien"]
// enleves est ["tambour"]

// supprime 2 éléments à partir de l'index 0, et insère "perroquet", "anémone" et"bleu"
enleves = mesPoissons.splice(0, 2, "perroquet", "anémone", "bleu")
// mesPoissons est ["perroquet", "anémone", "bleu", "trompette", "chirurgien"]
// enleves est ["scalaire", "clown"]
```

```javascript
const mesPoissons = ["perroquet", "anémone", "bleu", "trompette", "chirurgien"]
// on retire trois éléments à partir de l'indice 2
let enleves = mesPoissons.splice(2)
// mesPoissons vaut ["perroquet", "anémone"]
// enleves vaut ["bleu", "trompette", "chirurgien"]
```

### `slice`

Il existe aussi la méthode `slice` (plus simple et "moins puissante") qui fonctionne comme `slice` pour les strings.   
`slice` ne modifie pas l'array, mais crée une copie.

```javascript
const mesPoissons = ["scalaire", "clown", "mandarin", "chirurgien", "bleu"]
let poissonsChoisis = mesPoissons.slice(2)
// poissonsChoisis ["mandarin", "chirurgien", "bleu"]
// mesPoissons - ["scalaire", "clown", "mandarin", "chirurgien", "bleu"]

poissonsChoisis = mesPoissons.slice(2, 3)
// poissonsChoisis ["mandarin"]
// mesPoissons - ["scalaire", "clown", "mandarin", "chirurgien", "bleu"]

poissonsChoisis = mesPoissons.slice(0, 3)
// poissonsChoisis [ 'scalaire', 'clown', 'mandarin' ]
// mesPoissons - ["scalaire", "clown", "mandarin", "chirurgien", "bleu"]
```

## Renverser l'ordre des éléments

```javascript
const myArray = ["un", "deux", "trois"]
myArray.reverse()

console.log(myArray) // ["trois", "deux", "un"]
```

Méthode `reverse` modifie le tableau.

Il existe aussi méthode `sort` qui permet de changer l'ordre des éléments selon un critère défini, nous la verrons dans le support suivant.

## Parcourir la liste

### boucle `for` classique

```javascript
const shoppingList = ["2 t-shirts", "un short", "un pareo"]

for (let i = 0; i <= shoppingList.length - 1; i++) {
  console.log(`J'ai besoin d'acheter ${shoppingList[i]}`)
}

/* affiche :
J'ai besoin d'acheter 2 t-shirts
J'ai besoin d'acheter un short
J'ai besoin d'acheter un paréo
*/
```

### méthode moderne 😍, boucle `for ... of`

```javascript
const shoppingList = ["2 t-shirts", "un short", "un paréo"]

for (let item of shoppingList) {
  alert(`J'ai besoin d'acheter ${item}`)
}

/* affiche :
J'ai besoin d'acheter 2 t-shirts
J'ai besoin d'acheter un short
J'ai besoin d'acheter un paréo
*/
```

### méthode `forEach`

Le paramètre de la méthode `forEach` est une fonction (fonction "callback", dans l'exemple ci-dessous `iterationFunction`) qui sera utilisée pour chaque élément du tableau. La fonction `iterationFunction` a des paramètres. Son premier paramètre est la valeur de l'élément du tableau en cours de traitement.

```javascript
const shoppingList = ["2 t-shirts", "un short", "un paréo"]

const iterationFunction = (el) => {
  // el - valeur de l'élément du tableau en cours de traitement
  console.log(`J'ai besoin d'acheter ${el}.`)
}

/* affiche :
J'ai besoin d'acheter 2 t-shirts.
J'ai besoin d'acheter un short.
J'ai besoin d'acheter un paréo.
*/
```

La fonction `iterationFunction` a aussi accès à l'indice de l'élément du tableau en cours de traitement - ce sera son deuxième paramètre.

```javascript
const shoppingList = ["2 t-shirts", "un short", "un paréo"]

const iterationFunction = (el, index) => {
  // el - valeur de l'élément du tableau en cours de traitement
  // index - l'indice de l'élément du tableau en cours de traitement.
  console.log(`(${index}) J'ai besoin d'acheter ${el}.`)
}

/* affiche :
(1) J'ai besoin d'acheter 2 t-shirts.
(2) J'ai besoin d'acheter un short.
(3) J'ai besoin d'acheter un paréo.
*/
```

Et enfin, avec son 3e paramètre, `iterationFunction` a accès au tableau sur lequel la méthode forEach est appliquée.

```javascript
const iterationFunction = (el, index, array) => {
  console.log(`(${index + 1}/${array.length}) J'ai besoin d'acheter ${el}`)
}
shoppingList.forEach(iterationFunction)

/* affiche :
(1/3) J'ai besoin d'acheter 2 t-shirts
(2/3) J'ai besoin d'acheter un short
(3/3) J'ai besoin d'acheter un paréo
*/
```

## Concatener des arrays

La méthode `concat` fusionne deux ou plusieurs tableaux en les concaténant. Cette méthode ne modifie pas les tableaux existants, elle renvoie un nouveau tableau qui est le résultat de l'opération.

```javascript
const array1 = ["a", "b", "c"]
const array2 = ["d", "e", "f"]
const array3 = array1.concat(array2)

console.log(array3)
// ["a", "b", "c", "d", "e", "f"]
```

## String ↔️ Array `split` & `join`

Il est pratique de savoir comment transformer les strings en arrays et vice versa. Pour cela, nous avons deux méthodes :
- `split` qui opère sur les valeurs de type `"string"`
- `join` qui opère sur les arrays


```javascript
const arrayFromString = "hello".split("")
// ['h','e','l','l','o']
arrayFromString.reverse().join("")
// 'olleh'
arrayFromString.join("-")
// 'o-l-l-e-h'
arrayFromString.join(" ")
// 'o l l e h'
"Nous aimons JavaScript".split(" ")
// [ 'Nous', 'aimons', 'JavaScript' ]

"Nous  aimons    JavaScript".split(/\s+/)
// [ 'Nous', 'aimons', 'JavaScript' ]
```

## Exercices

- [Arrays (1)](https://codepen.io/alyra/pen/RwrqEbg) | [solution](https://codepen.io/alyra/pen/49924ef5f70f5aa180939fa4577423b0)
- [Arrays Magic Ball](https://codepen.io/alyra/pen/QWyJzbJ) | [solution](https://codepen.io/alyra/pen/150130653967a99107d42d5bf2ad3837)
- [js quizzes - arrays](https://javascript-quizzes.netlify.app/arrays)
