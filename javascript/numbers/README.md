

# Type `"numbers"` - méthodes utiles

## Vérification

Les valeurs transmises par l'utilisateur, via un formulaire par exemple, sont souvent de type `"string"`. 
Nous avons besoin des méthodes qui vérifient si un string contient une valeur numérique ?

Pour cela nous pouvons utiliser des fonctions `isNaN()` ou `isFinite()`. 

`isNaN` nous donnera `true` si le string **n'est pas** une valeur numérique, `NaN` correspondant à "**not** a number"

```javascript
isNaN("haha") // true
isNaN("3 chatons") // true
```

Par contre :

```javascript
isNaN("78") // false
isNaN("3") // false
```

`isFinite` agit de la façon inverse, et donne `true` pour les valeur numériques :

```javascript
isFinite("78") // true
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

On peut aussi utiliser la méthode `.toFixed()` comme ci-dessous. Attention, le résultat sera de type `"string"`.

```javascript
(2.789).toFixed(1)
// '2.8'
(2.789).toFixed(0) 
// '3'
```

### Les nombres aléatoires

`Math.random()` génère un nombre aléatoire entre 0 (inclut) et 1 (exclu) [0, 1)

À l'aide des opérations arithmétiques et d'autres méthodes disponibles pour nombres nous pouvons obtenir des nombres aléatoires des intervalles différentes.

Par exemple afin, d'obtenir les nombres d'intervalle `[a, b)` :

```javascript
(b - a) * Math.random() + a // [a, b)
```

Afin d'obtenir les nombres entières d'un intervalle : `a, a+1, ...., b`

```javascript
Math.floor(Math.random * (b + 1 - a)) + a // `a, a+1, ...., b`
```

```javascript
Math.floor(Math.random * 6) + 1 // comme si on lancé un dé, 6 résultats possible : 1, 2, 3, 4, 5 ou 6
```

```javascript
Math.floor(Math.random * 2) // comme si on lancé une monnaie, deux résultats possible : 0 ou 1
```

### Valeurs maximale et minimale

`Math.max(num1, num2)`
`Math.min(num1, num2, num3)`

```javascript
Math.max(10, 35, 6.7) // 35
Math.min(8 * 7, 6 * 9) // 54
Math.max(8 * 7, 6 * 9) // 56
```

### Conversion en système binaire, hexadécimal, etc.

`().toString(base)`

le paramètre `base` prend des valeur de `2` au `36`, sa valeur par défaut et `10`

````javascript
(255).toString(16)  // 'ff'
(255).toString(2)   // '11111111'
```javascript

[JS - Tours - 1a](https://jstours-1a.netlify.app/)
````

## Exercices

[JavaScript Quizzes - Numbers](https://javascript-quizzes.netlify.app/numbers)
