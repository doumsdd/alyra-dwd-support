# Méthodes pour numbers

## Vérification

Comment vérifier si un string est une valeur numérique ?

C'est particulièrement important dans le cas d'entrée d'utilisateur.

Nous pouvons utiliser `isNaN()` et `isFinite()`

```javascript
isNaN("5") // false
isNaN("haha") // true
isNaN("3 chatons") // true

isFinite("5") // true
isFinite("haha") // false
isFinite("3 chatons") // false
```

### Conversion en nombres entières

On utilise la fonction `parseInt(string, 10)` pour convertir en nombres entières comme ceci :

```javascript
parseInt("3 chatons", 10) // 3
parseInt("24chiots", 10) // 24
parseInt("3.75 pommes", 10) // 3
parseInt("12rem", 10) // 12
```

Il existe aussi `parseFloat()`

```javascript
parseFloat("3.75 pommes") // 3.75
parseFloat("12.5rem") // 12.5
```

`parseInt` avec la base différente que 10 permet de convertir depuis le système de `base` vers le système décimal :

```javascript
parseInt("ff", 16) // 255
parseInt("11111111", 2) // 255
```

### Comment arrondir les nombres ?

- `Math.round(number)` - vers le nombre entier le plus proche
- `Math.floor(number)` - vers le bas (floor = sol)
- `Math.ceil(number)` - vers le haut (ceil = plafond)
- `Math.trunc(number)` - coupe tout ce qui suit `.`

```javascript
Math.round(2.6) // 3
Math.floor(2.6) // 2
Math.ceil(2.6) // 3
Math.trunc(2.6) // 2
Math.round(-2.6) // -3
Math.floor(-2.6) // -3
Math.ceil(-2.6) // -2
Math.trunc(-2.6) // -2
```

On peut aussi utiliser la méthode `.toFixed()` comme ci-dessous. Attention, le résultat sera de type "string".

```javascript
;(2.789)
  .toFixed(1)(
    // '2.8'
    2.789
  )
  .toFixed(0) // '3'
```

### Les nombres aléatoire

`Math.random()` génére un nombre aléatoire entre 0 (inclu) et 1 (exclu) [0, 1)

```javascript
Math.floor(Math.random * 6) + 1 // comme si on lancé un dé, 6 résultats possible : 1, 2, 3, 4, 5 ou 6
```

```javascript
Math.floor(Math.random * 2) // comme si on lancé une monnaie, deux résulats possible : 0 ou 1
```

### Valeurs maximale et minimale

`Math.max(num1, num2)`
`Math.min(num1, num2, num3)`

```javascript
Math.max(10, 35, 6.7) // 35
Math.min(8 * 7, 6 * 9) // 54
Math.max(8 * 7, 6 * 9) // 56
```

### Convertion en système binaire, héxadecimal, etc.

`().toString(base)`

le paramètre `base` prend des valeur de `2` au `36`, sa valeur par défault et `10`

````javascript
(255).toString(16)  // 'ff'
(255).toString(2)   // '11111111'
```javascript

[JS - Tours - 1a](https://jstours-1a.netlify.app/)
````

## Exercices

[JavaScript Quizzez - Numbers](https://javascript-quizzes.netlify.app/numbers)
