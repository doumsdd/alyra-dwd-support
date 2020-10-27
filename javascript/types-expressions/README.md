# JavaScript - premiers pas avec types et expressions

Bienvenue dans le monde de JavaScript :) Nous allon commencer notre aventure avec cette language de programmation, disponible dans le navigateur. Nous allons commencer par des bases qui nous permetterons ensuite de créer des interfaces utilisateur intéractives. 

Nous allons commencer par un aperçu des différents types des données et comment on travaille avec eux. Dans JavaScript ils existe plusieurs types de données simples (nommés primitifs) ainsi que des objets et des fonctions (que nous allons découvrir un peu plus tard).

_Qu'est que ça veut dire type de données ? Pourquoi en parler ?_ Voici un exemple. Avec JavaScript nous pouvons executer les opérations arythmetiques, par exemple `1 + 2` sera évalué en tant que `3`. On peut aussi effectuer des opérations sur les chaines de carectères, par exemple `"Java" + "String"` sera évalué en tant que `"JavaScript"`. De la même façon `"1" + "2"` donne `"12"`. Vous voyez la différence entre `"1" + "2"` et `1 + 2` ? Quel sera le résultat de `"1" + 2` 🧐 ? Vous saurez répondre à cette question suite à ce premier cours de JavaScript !

## Types de données :

Vous pouvez ouvrir votre _terminal_ est taper `node`. Pour sortir de mode "node", tapez `.exit` Pour vérifier le "type" nous disposons de la fonction `typeof` qui retourne le type.

### (primitif) **number**,

ex. `2`, `33.6`, `-10`, `1e5`, `Infinity`, `-Infinity`, `NaN`

```javascript
typeof(5)
// 'number'
```

### (primitif) **string**

```javascript
"Bonjour tout le monde !"
"Hello world!"
"a"
"a"
`a`
("123")
"123"
`123`
'Je m'appelle .. '
"Je m'appelle .."
`Je m'appelle ..`
("Bonjour et \
Bonsoir")

"Je pense que 320px donnera " +
  320 / 16 +
  "rems"`Je pense que 320px donnera ${320 / 16}rems``Bonjour et
Bonsoir`
```

```javascript
typeof "Bonjour tout le monde !"
// 'string'
typeof "123"
// 'string'
```

### (primitif) **boolean**,

Il y deux valeurs possibles : `true` ou `false`

```javascript
typeof true // 'boolean'
typeof false // 'boolean'
typeof (10 > 2) // 'boolean'
10 > 2 // true
typeof (10 == 2) // 'boolean'
10 == 2 // false
typeof (10 != 2) // 'boolean'
10 != 2 // true
```

### (primitif) **undefined**

```javascript
typeof a
// 'undefined'
typeof paulina
// 'undefined'
```

<hr/>

### D'autres types

Dont nous ne parlons pas encore ajourd'hui

- (primitif) **null**

- (primitif) **BigInt**

- (primitif) **Symbol**

- **Object**

- **Function**

## Expressions

### Numbers

addition `+`  
soustraction `-`  
multiplication `*`  
division `/`  
modulo `%` - le reste de division  
puissance `**`

```javascript
6 % 3 // 0
6 % 2 // 0
(3 % 2) - // 1
(3 % 2) // -1
```

```javascript
6 ** 3 // 216 puisque 6*6*6
5 ** 4 // 625 puisque 5*5*5*5
```

### Strings

addition +

```javascript
"Hello" + " " + "World" + "!"
// Hello World!
```

### Booleans

negation `!`

```javascript
!true
// false
!false
// true
```

or / ou `||`

```javascript
true || true
//true
true || false
//true
false || true
//true
false || false
//false
```

and / et `&&`

```javascript
true && true
//true
true && false
//false
false && true
//false
false && false
//false
```

On peut utiliser d'autre valeurs que `true` et `false` dans le context boolean. Souvent on utilise les opérateurs `!`, `||` et `&&` avec valeurs de différents types.

Il faut savoir que certaines valeurs vont être **falsy** - évaluées _comme_ fausses quand elles se trouvent dans un contexte booléen. Les autres valeurs vont être **truthy** - évaluées _comme_ vraies, quand elles se trouvent dans un contexte booléen.

### Falsy (Valeurs de type fausses)

```javascript
false
null
undefined
0
NaN
;("")
""``
```

Et tout ce qui n'est pas **falsy** et **truthy** !

```javascript
null || undefined
//undefined (falsy)
!0
//true
```

## `||`

```javascript
0 || undefined || ""
/* va de gauche à droite et arrête toi à la première valeur truthy, s'il y en a pas - la dernière valeur */
// ''
0 || undefined || "Lunch" || ""
// "Lunch"
"Burrito" || "Gaspacho" || "Paëlla"
// "Burrito"
```

## `&&`

```javascript
0 && undefined && ""
/* va de gauche à droite et arrête toi à la première valeur falsy, s'il y en a pas - la dernière valeur */
// 0
"Lunch" && 0 && undefined && ""
// 0
"Burrito" && "Gaspacho" && "Paëlla"
// "Paëlla"
```

## Peut on soit-même convertir un type vers l'autre ?

Pour l'instant, nous avons vu que JavaScript convertit les types dans certaines situations.  
Est-ce possible de "imposer" cette conversion ?  
Tout à fait :

### Number

```javascript
Number("1") + // 1
  "1" // 1

Number("hello") + // NaN
  "hello" // NaN

Number(true) + // 1
  true // 1

Number(false) + // 0
  false // 0

Number(null) + // 0
  null // 0

Number("   ") + // 0
  "   " // 0
```

### String

```javascript
String(12)
// '12'
String(true)
// 'true'
```

### Boolean

```javascript
Boolean(1)
// true
Boolean(0)
// false
Boolean(null)
// false
Boolean(undefined)
// false
Boolean("")
// false
```

La conversion des types vers "numbers" a lieu aussi quand nous executons certaines opérations :

- comparaison (>, <, <=,>=)
- `(- + * / % )` (sauf `+` si un des opérands est de type 'string')
- `+` (opérateur unaire qui convertit en "number"
- `==` et `!=` mais **il n'y a pas** de conversion pour `===` et `!==`

```javascript
"1" == 1 // true
"1" === 1 // false
"2" != 3 // true
"2" !== 3 // true
"3" !== 3 // true
"3" != 3 // false
```

Pour en savoir plus [JavaScript Equality Table](https://dorey.github.io/JavaScript-Equality-Table/)

## Opérateur conditionnel (ternaire)

syntaxe `condition ? exprSiVrai : exprSiFaux`

```javascript
10 > 4 ? "pain au chocolat" : "chocolatine"
// pain au chocolat
```

[JavaScript Quizz](Bienvenue dans le monde de JavaScript :)

Nous allons commencer par un aperçu des différents types des données et comment on travaille avec eux.

## Types de données :

(Vous pouvez ouvrir votre _terminal_ est taper `node`. Pour sortir de mode "node", tapez `.exit`)

Pour vérifier le "type" nous disposons de la fonction `typeof` qui retourne le type.

### (primitif) **number**,

ex. `2`, `33.6`, `-10`, `1e5`, `Infinity`, `-Infinity`, `NaN`

```javascript
typeof 5
// 'number'
```

### (primitif) **string**

```javascript
"Bonjour tout le monde !"
"Hello world!"
"a"
"a"`a`
;("123")
"123"`123`
;("Je m'appelle .. ")
"Je m'appelle .."`Je m'appelle ..`
;("Bonjour et \
Bonsoir")

"Je pense que 320px donnera " +
  320 / 16 +
  "rems"`Je pense que 320px donnera ${320 / 16}rems``Bonjour et
Bonsoir`
```

```javascript
typeof "Bonjour tout le monde !"
// 'string'
typeof "123"
// 'string'
```

### (primitif) **boolean**,

Il y deux valeurs possibles : `true` ou `false`

```javascript
typeof true // 'boolean'
typeof false // 'boolean'
typeof (10 > 2) // 'boolean'
10 > 2 // true
typeof (10 == 2) // 'boolean'
10 == 2 // false
typeof (10 != 2) // 'boolean'
10 != 2 // true
```

### (primitif) **undefined**

```javascript
typeof a
// 'undefined'
typeof paulina
// 'undefined'
```

<hr/>

### D'autres types

Dont nous ne parlons pas encore ajourd'hui

- (primitif) **null**

- (primitif) **BigInt**

- (primitif) **Symbol**

- **Object**

- **Function**

## Expressions

### Numbers

addition `+`  
soustraction `-`  
multiplication `*`  
division `/`  
modulo `%` - le reste de division  
puissance `**`

```javascript
6 % 3 // 0
6 % 2 // 0
;(3 % 2) - // 1
  (3 % 2) // -1
```

```javascript
6 ** 3 // 216 puisque 6*6*6
5 ** 4 // 625 puisque 5*5*5*5
```

### Strings

addition +

```javascript
"Hello" + " " + "World" + "!"
// Hello World!
```

### Booleans

negation `!`

```javascript
!true
// false
!false
// true
```

or / ou `||`

```javascript
true || true
//true
true || false
//true
false || true
//true
false || false
//false
```

and / et `&&`

```javascript
true && true
//true
true && false
//false
false && true
//false
false && false
//false
```

On peut utiliser d'autre valeurs que `true` et `false` dans le context boolean. Souvent on utilise les opérateurs `!`, `||` et `&&` avec valeurs de différents types.

Il faut savoir que certaines valeurs vont être **falsy** - évaluées _comme_ fausses quand elles se trouvent dans un contexte booléen. Les autres valeurs vont être **truthy** - évaluées _comme_ vraies, quand elles se trouvent dans un contexte booléen.

### Falsy (Valeurs de type fausses)

```javascript
false
null
undefined
0
NaN
;("")
""``
```

Et tout ce qui n'est pas **falsy** et **truthy** !

```javascript
null || undefined
//undefined (falsy)
!0
//true
```

## `||`

```javascript
0 || undefined || ""
/* va de gauche à droite et arrête toi à la première valeur truthy, s'il y en a pas - la dernière valeur */
// ''
0 || undefined || "Lunch" || ""
// "Lunch"
"Burrito" || "Gaspacho" || "Paëlla"
// "Burrito"
```

## `&&`

```javascript
0 && undefined && ""
/* va de gauche à droite et arrête toi à la première valeur falsy, s'il y en a pas - la dernière valeur */
// 0
"Lunch" && 0 && undefined && ""
// 0
"Burrito" && "Gaspacho" && "Paëlla"
// "Paëlla"
```

## Peut on soit-même convertir un type vers l'autre ?

Pour l'instant, nous avons vu que JavaScript convertit les types dans certaines situations.  
Est-ce possible de "imposer" cette conversion ?  
Tout à fait :

### Number

```javascript
Number("1") + // 1
  "1" // 1

Number("hello") + // NaN
  "hello" // NaN

Number(true) + // 1
  true // 1

Number(false) + // 0
  false // 0

Number(null) + // 0
  null // 0

Number("   ") + // 0
  "   " // 0
```

### String

```javascript
String(12)
// '12'
String(true)
// 'true'
```

### Boolean

```javascript
Boolean(1)
// true
Boolean(0)
// false
Boolean(null)
// false
Boolean(undefined)
// false
Boolean("")
// false
```

La conversion des types vers "numbers" a lieu aussi quand nous executons certaines opérations :

- comparaison (>, <, <=,>=)
- `(- + * / % )` (sauf `+` si un des opérands est de type 'string')
- `+` (opérateur unaire qui convertit en "number"
- `==` et `!=` mais **il n'y a pas** de conversion pour `===` et `!==`

```javascript
"1" == 1 // true
"1" === 1 // false
"2" != 3 // true
"2" !== 3 // true
"3" !== 3 // true
"3" != 3 // false
```

Pour en savoir plus [JavaScript Equality Table](https://dorey.github.io/JavaScript-Equality-Table/)

## Opérateur conditionnel (ternaire)

syntaxe `condition ? exprSiVrai : exprSiFaux`

```javascript
10 > 4 ? "pain au chocolat" : "chocolatine"
// pain au chocolat
```

[JS - Tours - 1](https://javascript-quizzes.netlify.app/types)
