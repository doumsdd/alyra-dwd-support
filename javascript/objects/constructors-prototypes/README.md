# Constructors & Prototypes

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

Jaba, Zork, Deej, Plok est vient d'avoir 100 ans et ils doivent désormais être ajouter dans le registre des aliens.

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

```javascript
function Alien(name, age = 100) {
  this.name = name
  this.age = age
}
```

Et voici comment on crée des nouvelles instances des Aliens

```javascript
const alien1 = new Alien("Deej", 200)
const alien2 = new Alien("Flax")
```

![](https://assets.codepen.io/4515922/proto.png)

Au lieu de répéter le code ci-dessus pour chaque alien, il est possible de créer une fonction qui va nous servir pour le constructeur de chaque alien :

**Remarques :**

- Les noms des functions constructor commencent par une lettre en majuscules (c'est une convention)
- Les fonctions contructor doivent être appelées avec `new` (attention, oublie de `new` provoque une erreur `Uncaught TypeError: Cannot set property ... of undefined`)

[[[pen slug-hash='oNbKENV' height='300' theme-id='1']]]

# Prototype

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

[[[pen slug-hash='abdeYWv' height='300' theme-id='1']]]

On a plus de contrôle en utilisant [`Object.defineProperty`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Object/defineProperty)

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
  ;`Salut tout le monde, c'est ${this.name.toUpperCase()} qui parle`
}
alien1.sayHi() // Salut tout le monde, c'est FLAX qui parle
delete alien1.sayHi
alien1.sayHi() // Salut ! Mon nom est Flax. J'ai 100 ans.
```

![](https://assets.codepen.io/4515922/heritage.png)

---

## Exercices

- [js quizzes Constructors & Prototypes](https://javascript-quizzes.netlify.app/object-constructor)
