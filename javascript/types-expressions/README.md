# JavaScript - premiers pas avec types et expressions

Bienvenue dans le monde de JavaScript :) 

Nous allons commencer notre aventure par un aperçu des différents types des données. Nous allons apprendre comment on travaille avec eux. Dans JavaScript il existe plusieurs types de données simples (nommés primitifs) ainsi que des objets et des fonctions (que nous allons découvrir un peu plus tard).

_Qu'est que ça veut dire type de données ? Pourquoi devons nous en parler ?_ Voici un exemple. Avec JavaScript nous pouvons executer les opérations arithmétiques, par exemple `1 + 2`. Comme vous pouvez deviner `1 + 2` sera évalué en tant que `3`. 

On peut aussi effectuer des opérations sur les chaines de caractères, par exemple `"Java" + "String"` sera évalué en tant que `"JavaScript"`. De la même façon `"1" + "2"` donne `"12"`. Vous voyez la différence entre `"1" + "2"` et `1 + 2` ? Quel sera le résultat de `"1" + 2` 🧐 ? Vous saurez répondre à cette question suite à ce premier cours de JavaScript !

## Types de données :

Nous allons utiliser JavaScript avec Node.js que vous avez installé et qui est disponible dans votre terminal. Vous pouvez alors ouvrir votre terminal et taper `node`. Pour sortir de mode "node", tapez `.exit` Pour vérifier le "type" nous disposons de la fonction `typeof` qui retourne le type.

### (primitif) **number**

Voici quelques exemples de type primitif "number" :

```javascript
2
33.6
-10
1e5
Infinity
-Infinity
NaN

typeof(5)
// 'number'
```

Essayer de taper `typeof(..)` pour chaque de ces exemples donnera le résultat `"number"`.
On effectuant des opérations arithmétiques sur les données de type "number" nous obtenons des résultat de type `"number"`, par exemple :

```javascript
typeof(2 + 4) // 'number'
typeof(3 * 2) // 'number'
typeof(0 / 0) // 'number'
typeof(1 / 0) // 'number'
typeof(-1 / 0) // 'number'
```

### (primitif) **string**

Le chaine de caractères (`"string"`) est entourée par des guillemets, comme dans les exemples suivantes :

```javascript
"Bonjour tout le monde !"
"Hello world!"
"a"
'a'
`a`
"123"
'123'
`123`

//'Je m'appelle Paulina'
"Je m'appelle Paulina"
`Je m'appelle Paulina`
'Je m\'appelle Paulina'

("Bonjour et \
Bonsoir")

"Je pense que 320px donnera " + 320 / 16 + "rems"

`Je pense que 320px donnera ${320 / 16}rems`

`Bonjour et
Bonsoir`

"Bonjour et \
Bonsoir"
```

```javascript
typeof("Bonjour tout le monde !")
// 'string'
typeof("123")
// 'string'
```

### (primitif) **boolean**,

Le troisième type primitif, particulièrement important est `"boolean".` Il prend une des deux valeurs possibles : `true` (vrai)  ou `false` (faux).
Ceci permet de conditionner le comportement de notre script. 

Par exemple, si l'utilisateur est connecté l'interface affiche son tableau de bord, dans le cas contraire l'interface affiche le formulaire de connexion.

Quels sont des exemples du type `"boolean"` ? Ce sont `true` est `false` mais aussi tous les résultat de comparaison, tels que `10 > 2` ou `-3 < -4`. 


```javascript
typeof(true) // 'boolean'
typeof(false) // 'boolean'
typeof(10 > 2) // 'boolean'
10 > 2 // true
typeof (10 == 2) // 'boolean'
10 == 2 // false
typeof (10 != 2) // 'boolean'
10 != 2 // true
```

### (primitif) **undefined**

Quand JavaScript rencontre une chaine de caractères qui n'est pas entourée par des guillement, il cherche la fonction ou la variable qui est identifiée avec cette chaine de carectère. (Nous allons parles des variables et des foncions très bientôt). Si JavaScript ne trouve pas de valeur qui correspond à notre chaine, son type est `"undefined"`.

```javascript
typeof a
// 'undefined'
typeof paulina
// 'undefined'
```

<hr/>

### D'autres types

Dont nous ne parlons pas encore aujourd'hui

- (primitif) **null**, `null` est un type primitif et pourtant `typeof(null)` donne `"object"`

- (primitif) **BigInt**

- (primitif) **Symbol**

- **Object**

- **Function**

## Expressions

Nous parlons d'expression JavaScript quand nous démandons à JavaScript de nous **donner un résultat**. par exemple `1 + 2` est une expression, son résultat est 3 (de type "number"). Regardons ensemble d'autres exemples des expressions JavaScript.

### Numbers

Plusieurs expressions JavaScript peuvent être composées avec des opérations arithmétiques, telles que :

- addition, opérateur `+`  
- soustraction, opérateur `-`  
- multiplication, opérateur `*`  
- division, opérateur `/`  
- modulo, opérateur `%` - le reste de division  
- puissance, opérateur `**`

```javascript
6 % 3 // 0
6 % 2 // 0
3 % 2 // 1
-3 % 2 // -1
```

```javascript
6 ** 3 // 216 puisque 6*6*6
5 ** 4 // 625 puisque 5*5*5*5
```

### Strings

Dans le contexte des `"string"` l'opérateur qui est souvent utilisé est le `+` qui correspond à la concatenation. 

```javascript
"Hello" + " " + "World" + "!"
// Hello World!
```

### Booleans

Dans le contexte de valeurs du type `"boolean"`, nous utilisons souvent les opérateurs `!`, `||` est `&&`

**negation** `!`

```javascript
!true
// false
!false
// true
```

**or / ou** `||`

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

**and / et** `&&`

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

La conversion des types vers "numbers" a lieu aussi quand nous exécutons certaines opérations :

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

---

## Exercices

[JavaScript Quizz - Types & Expressions](https://javascript-quizzes.netlify.app/types)
