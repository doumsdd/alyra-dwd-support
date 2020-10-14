# Arrays - méthodes avec "callback" functions

## Méthode `map` 

![](https://assets.codepen.io/4515922/map.png)

```javascript
const mapCallback = (el, index, array) => ...
const newArray = myArray.map(mapCallback)
```

Chaque élément de myArray est passé par `mapCallback`, la nouvelle array contient les résultats d'évaluation de `mapCallback`


```javascript
const myArray = [1, 2, 3]
const arrayOfSquares = myArray.map(el => el * el)
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

Méthode `map` ne modifie pas l'array à laquelle elle est appliquée. Une nouvelle *array* est créée.

## Méthode `filter` 

![](https://assets.codepen.io/4515922/filter.png)

```javascript
const filterCallback = (el, index, array) =>  ...
const newArray = myArray.filter(filterCallback)
```

Chaque élément de myArray est passé par `filterCallback`, si le résultat est *truthy* l'élement reste, sinon l'élément est enlevé

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

Méthode `filter` ne modifie pas l'array à laquelle elle est appliquée. Une nouvelle *array* est créée.

## Méthode `find`

![](https://assets.codepen.io/4515922/find.png)

```javascript
const findCallback = (el, index, array) =>  ...
const element = myArray.find(findCallback)
```

```javascript
const myArray = [-1, 3, -3, 4, 6]
const element = myArray.find((el) => el > 2)
// 3
/* -1 -> -1 > 2 -> false -> ce n'est pas le bon élément
    3 ->  3 > 2 -> true  -> c'est bon ! je m'arrête et je retourne 3
*/
```

Il existe la méthode similaire `findIndex`

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

Méthode `some` retourne `true` si elle trouve un élément pour lequel la fonction callback est truthy

```javascript
const myArray = [-1, 3, -3, 4, 6]
const element = myArray.some((el) => el > 2)
// 1
/* -1 -> -1 > 2 -> false -> je continue
    3 ->  3 > 2 -> true  -> c'est bon ! je m'arrête et je retourne true
*/
```

Méthode `every` retourne `true` si la fonction callback est truthy pour tous les éléments

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
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// ["Dec", "Feb", "Jan", "March"]
```

Par défault en sortant les éléments sont transformés en string à la volée, ceci donne des résultats inattendus /o\

```javascript
const numbers = [1, 30, 4, 21, 100000];
numbers.sort();
console.log(numbers);
// [1, 100000, 21, 30, 4]
```

Pour y remedier, on utilise une fonction callback, qui "customize" le processus de trie


```javascript
const numbers = [1, 30, 4, 21, 100000];
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
});
console.log(numbers);
// [1, 4, 21, 30, 100000]
```

```javascript
function compareCallback(droit, gauche) {
  if (si droit inférieur à gauche selon notre critère personnalisé) {
    return -1; // ou une valeur négative, changement de l'ordre
  }
  if (si droit superieur à gauche selon notre critère personnalisé {
    return 1; // ou une valeur positive, pas de changement
  }
  // si droit et gauche sont égaux selon notre critère
  return 0;
}
```

La méthode `sort` modifie l'array.

# Exercices


 - [ja quizzes - arrays 2](https://javascript-quizzes.vercel.app/arrays-methods)
 - [JavaScript - methodes array](https://codepen.io/alyra/pen/dyGwaRK) | [solution](https://codepen.io/alyra/pen/48b9d965e9b54d5bbf035e118677186a)
 - [Arrays - sort](https://codepen.io/alyra/pen/NWxovVe) | [solution](https://codepen.io/alyra/pen/5221b2d16783781f591ff80e8f1679f5)