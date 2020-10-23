# Classes

```javascript
class Alien {
  constructor(name, age = 10) {
    this.name = name
    this.age = age
  }
  growUp(years = 1) {
    this.age += years
  }
  sayHi() {
    console.log(
      `Salut Terriens, mon nom est ${this.name}, j'ai ${this.age} ans.`
    )
  }
}

const alien1 = new Alien("Zork", 120)
alien1.sayHi() // Salut Terriens, mon nom est Zork, j'ai 120 ans.
```

Attention :

- pas de `()` dans la déclaration `class ClassName`
- pas de virgules
- la classe doit être appelée avec `new`, sinon `Uncaught TypeError: Class constructor cannot be invoked without 'new'`
- `sayHi() {...}` n'est pas équivalent à `sayHi = function() {...}`, comme en peut le voir dans l'exemple ci-dessous :

```javascript
class Alien {
  constructor(name, age = 10) {
    this.name = name
    this.age = age
  }
  // class field
  sayHi = function () {
    console.log(`Hello, mon nom est ${this.name} !`)
  }
  // méthode du prototype
  sayHi() {
    console.log(
      `Salut Terriens, mon nom est ${this.name}, j'ai ${this.age} ans.`
    )
  }
}
```

Quand on appelle  
`const alien1 = new Alien('Zork', 120)`  
un nouvel objet est crée, et la fonction `constructor` est executée.

Regardons ce qui affiche `console.log(alien1)`

![](https://assets.codepen.io/4515922/AlienClass.png)

Le code qu'on vient d'executer produit le résultat comparable au résultat de :

```javascript
// approche "CLASSique" ceci dit, avant l'introductions des classes ;)
function Alien(name, age = 10) {
  this.name = name
  this.age = age
}
Alien.prototype.growUp = function (years = 1) {
  this.age += years
}
Alien.prototype.sayHi = function (years = 1) {
  console.log(`Salut Terriens, mon nom est ${this.name}, j'ai ${this.age} ans.`)
}
```

# getters & setters

Classes ont getters et setters avec la syntaxe comme ceci :

```javascript
class Alien {
  constructor(name, age = 10) {
    this.name = name
    this.age = age
  }
  growUp(years = 1) {
    //...
  }
  sayHi() {
    //...
  }
  // getter isAdult
  get isAdult() {
    return this.age >= 300
  }
}

const alien1 = new Alien("Zork", 120)
alien1.isAdult // false.
alien1.growUp(200)
alien1.isAdult // true
```

Classes ont getters et setters avec la syntaxe comme ceci :

```javascript
class Url {
  constructor(protocol, domain) {
    this.protocol = protocol
    this.domain = domain
  }
  get fullLink() {
    return `${this.protocol}://${this.domain}`
  }
  set fullLink(value) {
    ;[this.protocol, this.domain] = value.split("://")
  }
}

const url = new Url()
url.fullLink = "https://codepen.io"
console.log(url)
```

![](https://assets.codepen.io/4515922/UrlClass.png)

# Champs de classe - class fields

Il est aussi possible d'ajouter des propriétés sans passer par la fonction `constructor`. Elles sont ajoutées pour chaque instance, et ne pas au niveau de prototype.

```javascript
class Alien {
  majorityAge = 300 // class field majorityAge
  constructor(name, age = 100) {
    this.name = name
    this.age = age
  }
}
const alien1 = new Alien("Plok")
```

![](https://assets.codepen.io/4515922/AlienMA.png)

Champs de classe sont initialisés **avant** le constructor, par conséquant

```javascript
class Alien {
  constructor(name, age = 100, majorityAge) {
    this.name = name
    this.age = age
    this.majorityAge = majorityAge
  }
  majorityAge = 300
}
const alien1 = new Alien("Deej", 200, 250)
alien1.majorityAge // 250 puisque contructor écrase la valeur de 300
```

**Attention** Dans le cas des classes dérivées (créées avec `extends`), champs de classe sont initialisés directement **après** `super()`

# focus sur this

```javascript
class Alien {
  constructor(name, age = 100) {
    this.name = name
    this.age = age
  }
  sayName() {
    console.log(`Mon nom est ${this.name}.`)
  }
  sayAge = () => {
    console.log(`J'ai ${this.age} ans.`)
  }
}
const alien1 = new Alien("Plok")
btn1 = document.getElementById("button-1")
btn2 = document.getElementById("button-2")
btn1?.addEventListener("click", alien1.sayName) // Mon nom est .
btn2?.addEventListener("click", alien1.sayAge) // J'ai 100 ans.
```

https://codepen.io/alyra/pen/oNxXqrN

```javascript
btn1?.addEventListener("click", alien1.sayName)
/*
btn1?.addEventListener("click", function() {
 // this correspindera au btn1
 console.log(`Mon nom est ${this.name}.`);
});
*/

btn1?.addEventListener("click", alien1.sayAge)
/*
alien1.sayAge est une arrow function, dans arrow function, this correspond à l'objet qui a défini cette fonction, alors alien1
*/
```

[Live coding - clock](https://codepen.io/alyra/pen/OJNVZxz)

# Classe héritage, classes dérivées

```javascript
class ChildClass extends ParentClass {
  // ...
}
```

```javascript
class Alien {
  constructor(name, age = 100) {
    this.name = name
    this.age = age
  }
  growUp(years = 1) {
    this.age += years
  }
  sayHi() {
    console.log(
      `Salut Terriens, mon nom est ${this.name}, j'ai ${this.age} ans.`
    )
  }
}
class SuperAlien extends Alien {
  goOnMission() {
    console.log(`Moi, Super Alien ${this.name}, je pars en mission sur Terre`)
  }
}
const superAlien1 = new SuperAlien("Froz")
superAlien1.goOnMission()
```

![](https://assets.codepen.io/4515922/superAlien.png)

Dans l'exemple ci-dessus, la class `SuperAlien` n'a pas de fonction `constructor`, en fait il est mis en place de la façon implicite

```
class SuperAlien extends Alien {
  /*
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  */
  goOnMission() {
    console.log(`Moi, Super Alien ${this.name}, je pars en mission sur Terre`)
  }
}
```

## super()

Parfois on veut modifier la fonction constructor, par exemple ajouter la propriété mission à `SuperAlien`.

```javascript
class SuperAlien extends Alien {
  /*
  on aurait pu tenter ceci :
  constructor(name, age, mission) {
    this.name = name
    this.age = age
    this.mission = mission
  }
  mais attention : Uncaught ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
  */
  // la version suivante et correcte
  constructor(name, age, mission) {
    // appelle constructor d'Alien
    super(name, age)
    this.mission = mission
  }
  goOnMission() {
    console.log(`Moi, Super Alien ${this.name}, je pars en mission sur Terre`)
  }
}
```

`super(...)` apelle le constructor de la classe parente, on **doit** l'utiliser dans le constructor de la classe enfant (si on la met en place explicitement).  
Par contre, on ne l'appelle pas en dehors de la fonction constructor.

`super(...)` dans le `constructor` doit être appelé le premier, avant l'utilisatio de `this` - sinon `Uncaught ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor`

## super.myParentMethod()

`super.myParentMethod()` permet d'appeler une méthode de la classe parent, par exemple

```javascript
class Alien {
  constructor(name, age = 100) {
    this.name = name
    this.age = age
  }
  sayHi() {
    console.log(`Hello, mon nom est ${this.name}, j'ai ${this.age} ans.`)
  }
}
class SuperAlien extends Alien {
  constructor(name, age, mission) {
    super(name, age)
    this.mission = mission
  }
  sayHi() {
    super.sayHi()
    console.log(`Je pars en mission ${this.mission}.`)
  }
}
const superAlien = new SuperAlien(
  "Froz",
  300,
  "diminuer la pollution des océans sur la planète Terre"
)
superAlien.sayHi()
/* console affichera :
Hello, mon nom est Froz, j'ai 300 ans.
Je pars en mission diminuer la pollution des océans sur la planète Terre.
*/
```

# méthodes et propriétés statiques

Le mot-clé static permet de définir une méthode statique d'une classe. Les méthodes statiques ne sont pas disponibles sur les instances d'une classe mais sont appelées sur la classe elle-même. Les méthodes statiques sont généralement des fonctions utilitaires (qui peuvent permettre de créer des objets par exemple). (source [MDN](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes/static))

```javascript
class Alien {
  static planet = "Meelaan Prime"
  static create(...args) {
    return new this(...args) // (**)
  }
  constructor(name, age) {
    this.name = name
    this.age = age
  }
}

const alien1 = new Alien("Deej", 200)
console.log(Alien.planet) // "Meelaan Prime"
console.log(alien1.planet) // undefined

const alien2 = Alien.create("Flax", 100)
```

Quand nous appelons `Alien.create('Flax', 100)`, `this` dans la ligne (\*\*) correspond à `Alien`

https://codepen.io/alyra/pen/vYGNLRg

# instanceof

Syntaxe

```javascript
object instanceof Constructor // true ou false
```

Ici on véfifie si Constructor est dans la la chaîne de prototypes de l'objet

par example :

```javascript
class Alien {
  /* ... */
}
class SuperAlien extends Alien {
  /* ... */
}
const alien1 = new Alien()
const superAlien1 = new SuperAlien()

alien1 instanceof Alien // true
superAlien1 instanceof SuperAlien // true
superAlien1 instanceof Alien // true
alien1 instanceof SuperAlien // false
alien1 instanceof Object // true
superAlien1 instanceof Object // true
```

---

## Exercices

- [js quizzes Classes](https://javascript-quizzes.netlify.app/object-constructor)
- [clock avec timezone](https://codepen.io/alyra/pen/jOqbqWR) | [solution](https://codepen.io/alyra/pen/8d564f5ac2540f244bf4eaff510ade8d)
- [classes - restaurant](https://codepen.io/alyra/pen/NWNqKRQ) | [solution](https://codepen.io/alyra/pen/c09c81be9f0e20a71c4c06f85779a47f)
