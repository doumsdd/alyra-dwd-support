# Constructors & Prototypes

## Constructor, opérateur `new`

Nous avons appris à définir et utiliser des objets :

```javascript
const alien1 = {
  name: "Jaba",
  age: 100,
  growUp(years = 1) {
    this.age += years
  },
  sayHi() {
    let message = "Salut !"
    message += this.name ? ` Mon nom est ${this.name}.` : ""
    message += this.age ? ` J'ai ${this.age} ans.` : ""
    console.log(message)
  },
  isAdult() {
    return this.age > 300
  },
}
```

Jaba, Zork, Deej, Plok est vient d'avoir 100 ans et ils doivent désormais être ajoutés dans le registre des aliens.

```javascript
const alien2 = {
  name: "Deej",
  age: 100,
  growUp(years = 1) {
    this.age += years
  },
  sayHi() {
    let message = "Salut !"
    message += this.name ? ` Mon nom est ${this.name}.` : ""
    message += this.age ? ` J'ai ${this.age} ans.` : ""
    console.log(message)
  },
}

// ...

const aliensRegistry = [alien1, alien2, alien3, alien4]
```

Nos objets aliens partagent les mêmes clés. La structure des données est des méthodes sont partagées par chacun d'eux. Au lieu de répéter le code ci-dessus pour chaque alien, il est possible de créer une fonction qui va nous servir pour le constructeur d'un alien.
La fonction "constructeur" qui nous permettra de créer plusieurs instances d'un objet avec la même structure (le mêmes clés). 

Voici un exemple, d'une fonction "constructeur", `Alien`. La convention veut que les constructeurs commencent par une letter en majuscule.

```javascript
function Alien(name, age = 100) {
  this.name = name
  this.age = age
}
```

Ensuite, nous utilisons un opérateur `new` pour créer des nouvelles instances des Aliens. Tous nos aliens partagent les mêmes clés avec des valeur différentes :

```javascript
const alien1 = new Alien("Deej", 200)
const alien2 = new Alien("Flax")
```

Quand la fonction `Alien` est appelée avec l'opérateur `new`, deux actions supplémentaires et implicites ont lieu :

- (\*) `this` est initié en tant que `{}`
- (\*\*) la fonction retourne `this`. (Je vous rappelle que normalement, quand appelée sans l'opérateur `new`, une fonction qui ne contient pas un `return` explicite, retourne `undefined`).

```javascript
function Alien(name, age = 100) {
// (*) this = {}
  this.name = name
  this.age = age
// (**) return this
}
```

**À retenir :**

- Les noms des functions constructeurs commencent par une lettre en majuscules (c'est une convention).
- Les fonctions contructeurs doivent être appelées avec `new` (attention, oublie de `new` provoque une erreur `Uncaught TypeError: Cannot set property ... of undefined`).

https://codepen.io/alyra/pen/oNbKENV


![](https://assets.codepen.io/4515922/proto.png)

## Prototype

On peut aussi associer les valeurs et les méthodes communes à toutes les instances. Nous allons les attacher au clé `prototype`.

```javascript
// constructor
function Alien(name, age = 100) {
  this.name = name
  this.age = age
}
Alien.prototype.growUp = function (years = 1) {
  this.age += years
}
Alien.prototype.sayHi = function () {
  let message = "Salut !"
  message += this.name ? ` Mon nom est ${this.name}.` : ""
  message += this.age ? ` J'ai ${this.age} ans.` : ""
  console.log(message)
}
```

https://codepen.io/alyra/pen/abdeYWv

La même chose peut être effectuer avec [`Object.defineProperty`.](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Object/defineProperty) Dans ce cas nous pouvons configurer le comportement de nos propriétés : 

```javascript
Object.defineProperty(Alien.prototype, 'sayHi', {
  value: function() {console.log('Hey!!')},
  enumerable: true, // false par défaut
  writable: true, // false par défaut
  configurable: true // false par défaut
}
```

- `enumerable` - la propriété va être listée (par exemple dans la boucle `for .. in`)
- `writable` - la valeur peut être modifiée (on peut associer une autre fonction pour sayHi
- `configurable` - on peut supprimer la propriété et changer les valeurs des `enumerable`, `writable` ou `configurable`

Attention, avec l'approche `Alien.prototype.sayHi = ...`, tous les trois `enumerable`, `writable` et `configurable` sont `true`

Nous pouvons aussi définir getters et setters. Ici on utilisera aussi la méthode `Object.defineProperty`. Au lieu d'utiliser 'value' on utilisera `get` et `set` :

```javascript
Object.defineProperty(Alien.prototype, "id", {
  get: function () {
    return "_" + this.name.toLowerCase()
  },
  enumerable: true,
})
```

## Héritage et chaîne de prototype


JavaScript est souvent décrit comme un langage basé sur les prototypes. Chaque objet a un prototype objet d'où il hérite des méthodes et des attributs. Plus précisément les objets ont une propriété cachée prototype, [[Prototype]],  qui est soit une référence vers un objet ou `null`.

Lorsqu'on tente d'accéder aux propriétés d'un objet, la propriété sera recherchée d'abord sur l'objet même, puis sur son prototype, puis sur le prototype du prototype et ainsi de suite.

```javascript
function Alien(name, age = 100) {
  this.name = name
  this.age = age
}
Alien.prototype.growUp = function (years = 1) {
  this.age += years
}
Alien.prototype.sayHi = function () {
  let message = "Salut !"
  message += this.name ? ` Mon nom est ${this.name}.` : ""
  message += this.age ? ` J'ai ${this.age} ans.` : ""
  console.log(message)
}

const alien1 = new Alien("Flax")
alien1.sayHi = function () {
  `Salut tout le monde, c'est ${this.name.toUpperCase()} qui parle`
}
alien1.sayHi() // Salut tout le monde, c'est FLAX qui parle
delete alien1.sayHi
alien1.sayHi() // Salut ! Mon nom est Flax. J'ai 100 ans.
```

![](https://assets.codepen.io/4515922/heritage.png)

---

## Exercices

- [js quizzes Constructors & Prototypes](https://javascript-quizzes.netlify.app/object-constructor)
