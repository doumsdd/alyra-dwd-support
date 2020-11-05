# Arrays - méthodes avec "callback" functions

Dans le cours précédent nous avons vu la méthode `forEach` qui opère sur un array et prend une fonction (*callback function*) en tant que le paramètre. Pour le rappel :

```javascript
const printList = (el, index) => {
   console.log(`${index + 1} - ${el}`)
}
const myArray = ["cumin", "curry", "chili"]
myArray.forEach(printList)
/*
1 - cumin
2 - curry
3 - chili
*/
```

Nous allons maintenant découvrir quelques méthodes supplémentaires qui facilitent la travail avec des tableaux. Nous allons parler de `map`, `filter`, `find`, `findIndex`, `every` `some` et `sort. 

## Méthode `map`

![](https://assets.codepen.io/4515922/map.png)

```javascript
const mapCallback = (el, index, array) => { ... }
const newArray = myArray.map(mapCallback)
```

Chaque élément de `myArray` est passé par la fonction `mapCallback`. La nouvelle array contient les résultats d'évaluation de `mapCallback` :

```javascript
const myArray = [1, 2, 3]
const arrayOfSquares = myArray.map((el) => el * el)
// [1, 4, 9]
/* 1 -> 1*1 -> 1
   2 -> 2*2 -> 4
   3 -> 3*3 -> 9
*/
```

```javascript
const myArray = [1, 2, 3]
const newArray = myArray.map((el, index) => el * index)
// [0, 2, 6]
/* 1,0 -> 1*0 -> 0
   2,1 -> 2*1 -> 2
   3,2 -> 3*2 -> 6
*/
```

Méthode `map` **ne modifie pas** l'array à laquelle elle est appliquée. Une nouvelle _array_ est créée.

## Méthode `filter`

![](https://assets.codepen.io/4515922/filter.png)

```javascript
const filterCallback = (el, index, array) =>  { ... }
const newArray = myArray.filter(filterCallback)
```

Chaque élément de myArray est passé par `filterCallback`, si le résultat est _truthy_ l'élément reste, sinon l'élément est enlevé.

```javascript
const myArray = [-1, 3, -3, 4, 6]
const newArray = myArray.filter((el) => el > 2)
// [3, 4, 6]
/* -1 -> -1 > 2 -> false -> élément n'est pas retenu
    3 ->  3 > 2 -> true  -> élément est retenu
   -3 -> -3 > 2 -> false -> élément n'est pas retenu
    4 ->  4 > 2 -> true  -> élément est retenu
    6 ->  6 > 2 -> true  -> élément est retenu
*/
```

Méthode `filter` **ne modifie pas** l'array à laquelle elle est appliquée. Une nouvelle _array_ est créée.

## Méthode `find`

![](https://assets.codepen.io/4515922/find.png)

```javascript
const findCallback = (el, index, array) =>  { ... }
const element = myArray.find(findCallback)
```

Les éléments de `myArray` sont passés, l'un après l'autre, par `findCallback`, si le résultat est _truthy_ l'élément est retourné et l'opération s'arrête.

```javascript
const myArray = [-1, 3, -3, 4, 6]
const element = myArray.find((el) => el > 2)
// 3
/* -1 -> -1 > 2 -> false -> ce n'est pas le bon élément
    3 ->  3 > 2 -> true  -> c'est bon ! je m'arrête et je retourne 3
*/
```

Il existe une méthode similaire `findIndex`, qui retourne l'index et pas l'élément du tableau. Les éléments de `myArray` sont passés, l'un après l'autre, par `findCallback`, si le résultat est _truthy_ l'index est retourné et l'opération s'arrête.

```javascript
const myArray = [-1, 3, -3, 4, 6]
const element = myArray.findIndex((el) => el > 2)
// 1
/* -1 -> -1 > 2 -> false -> ce n'est pas le bon élément
    3 ->  3 > 2 -> true  -> c'est bon ! je m'arrête et je retourne l'index (la position) d'élément 3 qui est égale à 1 
*/
```

## Méthodes `some` et `every`

Méthodes `some` et `every` retournent `true` ou `false`

```javascript
const someCallback = (el, index, array) =>  ...
const hasSome = myArray.some(someCallback)
```

Méthode `some` retourne `true` si elle trouve un élément pour lequel la fonction callback est *truthy*.

```javascript
const myArray = [-1, 3, -3, 4, 6]
const element = myArray.some((el) => el > 2)
// 1
/* -1 -> -1 > 2 -> false -> je continue
    3 ->  3 > 2 -> true  -> c'est bon ! je m'arrête et je retourne true
*/
```

Méthode `every` retourne `true` si la fonction callback est *truthy* pour tous les éléments.

```javascript
const myArray = [-1, 3, -3, 4, 6]
const hasBiggerThan2 = myArray.some((el) => el > 2)
// true
/* -1 -> -1 > 2 -> false -> je continue
    3 ->  3 > 2 -> true  -> c'est bon ! je m'arrête et je retourne true
*/
```

```javascript
const myArray = [-1, 3, -3, 4, 6]
const allBiggerThan2 = myArray.every((el) => el > 2)
// false
/* -1 -> -1 > 2 -> false -> je m'arrête et je retourne false
 */
```

```javascript
const myArray = [1, 3, 3, 4, 6]
const allPositive = myArray.every((el) => el >= 0)
// true
/* 1 -> 1 >= 0 -> true -> je poursuis la vérification
   3 -> 3 >= 0 -> true -> je poursuis la vérification
   3 -> 3 >= 0 -> true -> je poursuis la vérification
   4 -> 4 >= 0 -> true -> je poursuis la vérification
   6 -> 6 >= 0 -> true -> c'est true pour tous, alors je retourne true !!
*/
```

## Méthode `sort`

![](https://assets.codepen.io/4515922/sort.png)

```javascript
const months = ["March", "Jan", "Feb", "Dec"]
months.sort()
console.log(months)
// ["Dec", "Feb", "Jan", "March"]
```

Par défaut, JavaScript compare les équivalents "string" des éléments (coercion vers le type `"string"` à la volée). 
Attention, ceci donne des résultats inattendus 😱 :

```javascript
const numbers = [1, 30, 4, 21, 100000]
numbers.sort()
console.log(numbers)
// [1, 100000, 21, 30, 4]
```

Pour y remédier, on utilise une fonction callback, qui permet de "customiser" le processus de trie :


```javascript
function compareCallback(right, left) {
  if (si right est inférieur à left selon notre critère personnalisé) {
    return -1; // ou une valeur négative, changement de l'ordre
  }
  if (si right est supérieur à left selon notre critère personnalisé) {
    return 1; // ou une valeur positive, pas de changement
  }
  // si right et gauche sont égaux selon notre critère
  return 0;
}
```

```javascript
const numbers = [1, 30, 4, 21, 100000]
numbers.sort((right, left) => {
  if (right > left) {
    return 1 // valeur positive -> pas de changement
  } else if (right < left) {
    return -1 // valeur negative -> changement !!!
  } else {
    return 0 // valeur 0 -> pas de changement
  }
  /* sinon
  return right - left
  */
})
console.log(numbers)
// [1, 4, 21, 30, 100000]
```


La méthode `sort` **modifie** l'array.

# Exercices

- [ja quizzes - arrays 2](https://javascript-quizzes.netlify.app/arrays-methods)
- [JavaScript - methods array](https://codepen.io/alyra/pen/dyGwaRK) | [solution](https://codepen.io/alyra/pen/48b9d965e9b54d5bbf035e118677186a)
- [Arrays - sort](https://codepen.io/alyra/pen/NWxovVe) | [solution](https://codepen.io/alyra/pen/5221b2d16783781f591ff80e8f1679f5)
