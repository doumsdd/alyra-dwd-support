# Object methods & this

## Objects - méthodes

Les objets ne sont pas limités aux propriétés 'statiques', on peut aussi leur définir des méthodes (fonctions). Ci dessous nous ajoutons une clé `sayHi` à `alien`, `sayHi` est une fonction. Pour l'éxécuter nous allons appeler `alien.sayHi()`.

```javascript
const alien = {
  name: "Zork",
  age: 320,
}

alien.sayHi = function () {
  console.log(`Salutions Terriens`)
}

alien.sayHi()
```

On peut aussi mettre en place `sayHi` comme ceci

```javascript
const alien = {
  name: "Zork",
  age: 320,
  sayHi: function () {
    console.log(`Salutions Terriens`)
  },
}
```

ou la même chose avec la syntaxe raccourcie (_shorthand_)

```javascript
const alien = {
  name: "Zork",
  age: 320,
  sayHi() {
    // sayHi: function() -> sayHi()
    console.log(`Salutions Terriens`)
  },
}
```

```javascript
const alien = {
  name: "Zork",
  age: 320,
  sayHi() {
    console.log(`Salutions, Terriens`)
  },
  sayGoodBye() {
    console.log(`Soyez en paix, Humains`)
  },
}
```

## this

```javascript
const alien = {
  name: "Zork",
  age: 320,
  sayHi() {
    console.log(`Salutions Terriens, mon nom est ${this.name} !`)
  },
  getOlder(years = 1) {
    this.age += years
  },
}
```

Quand `sayHi` ou `getOlder` sont **appelées** en tant que des méthodes d'un objet, `this` correspondera à cet objet :

```javascript
alien.sayHi() // this devient alien -> Salutions Terriens, mon nom est Zork !
alien.name = "Jaba"
alien.sayHi() // alien a changé -> Salutions Terriens, mon nom est Jaba !
```

Par contre, `this` **ne correspond pas** à l'objet, si fonction est appelée directement

```javascript
const useOutside = alien.sayHi
/*
const useOutside = function () {
 console.log(`Salutions Terriens, mon nom est ${this.name} !`)
}
*/
useOutside() // Uncaught TypeError: Cannot read property 'name' of undefined
```

https://codepen.io/alyra/pen/bGEXNeb

`this` est un mot-clé spécial (keyword). Sa valeur change selon le contexte où il est utilisé. Voici quelques exemples :

### directement dans le script et pas dans le body d'une fonction

```javascript
"use strict"
console.log(this) // object window (navigateur)
console.log(this === window) // true
```

L'objet [`window`](https://developer.mozilla.org/fr/docs/Web/API/Window) représente une fenêtre contenant un document DOM.

```javascript
console.log(window.document === document) // true
window.scrollTo(0, 300)
console.log(window.scrollY) // 300
```

### dans une fonction classique (pas une arrow function) appelée directement (pas comme une méthode)

`this` devient `undefined`

```javascript
"use strict"
const hello = function () {
  console.log(this)
  console.log(this === window) // false
  console.log(this === undefined) // true
}
hello()

function bonjour() {
  console.log(this)
  console.log(this === window) // false
  console.log(this === undefined) // true
}
bonjour()
```

### dans une fonction fléchée (arrow function) appelée directement

`this` reste `window`, avec functions arrow, `this` répresent l'objet où la fonction était créée.

```javascript
"use strict"
const hello = () => {
  console.log(this) // window
  console.log(this === window) // true
  console.log(this === undefined) // false
}
hello()
```

### méthode d'un objet - fonction avec la syntaxe classique

`this` devient l'objet auquel on applique la méthode

```javascript
const alien = {
  name: "Deej",
  age: 100,
  isAdult() {
    // console.log(this) // (*)
    return this.age >= 300
  },
}
alien.isAdult() // this de la ligne (*) devient alien
```

### méthode d'un objet - fonction avec la syntaxe arrow

`this` comme il était, arrow function ne "bind" pas `this`, avec functions arrow, `this` répresent l'objet où la fonction était créée.

```javascript
const alien = {
  name: "Deej",
  age: 100,
  isAdult: () => {
    return this.age >= 300 // (**)
  },
}
alien.isAdult() // this de la ligne (**) est window
```

### fonction callback, syntaxe classique, dans addEventListener

`this` correspond à élément sur lequel on applique `addEventListener`

```javascript
document.body.addEventListener("click", function () {
  // this est égale à document.body
  this.classList.toggle("clicked")
})
```

```javascript
const alien = {
  name: "Deej",
  sayHi() {
    console.log(this.name)
  },
}
document.body.addEventListener("click", alien.sayHi)
/* le code ci-dessus et équivalent à 
document.body.addEventListener('click', function(){
  // this est égale à document.body
  console.log(this.name)
})
*/
```

https://codepen.io/alyra/pen/ExKYKVR

### fonction callback, syntaxe arrow, dans addEventListener

`this` comme il était, arrow function arrow function ne "bind" pas `this`, avec functions arrow, `this` répresent l'objet où la fonction était créée alors `window`

```javascript
document.body.addEventListener("click", () => {
  // this est égale à window
  this.classList.toggle("clicked")
})
```

```javascript
const alien = {
  name: "Deej",
  sayHiOnClick() {
    document.body.addEventListener("click", () => {
      alert(this.name)
    })
  },
}
alien.sayHiOnClick()
// en appellant `alien.sayHiOnClick()` this devient alien. En utilisant une fonction arrow comme callback dans addEventListener, this reste intacte, et toujours correspond à alien !
```

### fonction callback, syntaxe classique, dans setTimeout et setInterval

`this` devient window

### fonction callback, syntaxe arrow, dans setTimeout et setInterval

`this` répresent l'objet où la fonction fléchée a était créée.

## Binding

Il peut nous arriver de devoir changer le contexte de `this`. On a des outils pour cela, la méthode `bind`.

```html
<button id="say-hi-btn" type="button">Dis Bonjour</button>
```

```javascript
const alien = {
  name: "Zork",
  age: 320,
  sayHi() {
    console.log(`Salutions Terriens, mon nom est ${this.name} !`)
  },
}

const btn = document.getElementById("say-hi-btn")
btn.addEventListener("click", alien.sayHi)

/* ceci est équivalent à:

btn.addEventListener('click', function() {
  console.log(
    `Salutions Terriens, mon nom est ${this.name} !`
  );
})

*/
```

```javascript
const user = {
  name: "Marie",
  sayHi() {
    console.log(`Salut, je suis ${this.name}`)
  },
}

user.sayHi() // marche !
setTimeout(user.sayHi, 1000) // Salut, je suis undefined
```

https://codepen.io/alyra/pen/jOWgdqm

```javascript
// fix :
setTimeout(() => {
  user.sayHi()
}, 1000) // Salut, je suis Marie
setTimeout(user.sayHi.bind(user), 1000) // Salut, je suis Marie
```

# getters & setters

Afin de comprendre l'utilité de ce concept, regardons l'exemple suivaint :

```javascript
const website = {
  protocol: "https",
  domain: "alyra.fr",
  fullLink: "https://alyra.fr",
}
```

Quand le domain change, par exemple

`website.domain = alyra.com`

nous devons penser à changer `website.fullLink` en même temps.

Pour y rémédier on aurait pu, utiliser `fullLink` en tant qu'une méthode :

```javascript
const website = {
  protocol: "https",
  domain: "alyra.fr",
  fullLink() {
    return `${this.protocol}://${this.domain}`
  },
}

website.domain = "alyra.com"
website.fullLink() // donne https://alyra.com
```

Ca a l'air de résoudre le problème et souvant est une approche suffisante. Par contre, on n'est pas protégé contre la situation suivainte

```javascript
website.fullLink = "https://codepen.io"
console.log(website)
/*
{
  protocol: 'https',
  domain: 'alyra.fr',
  fullLink: 'https://codepen.io'
}
*/
```

Regardons une autre approche qui utilise les keywords `get` et `set`:

```javascript
const website = {
  protocol: "https",
  domain: "alyra.fr",
  get fullLink() {
    // quand je veux lire fullLink
    return `${this.protocol}://${this.domain}`
  },
  set fullLink(value) {
    // quand je veux écrire fullLink
    if (value.startsWith("http")) {
      const linkParts = value.split("://")
      this.protocol = linkParts[0]
      this.domain = linkParts[1]
    } else {
      alert(`fullLink doit commencer par 'http'`)
    }
  },
}
// pour lire (attention si on utilise getter, on accède au clé sans parentèses)
website.fullLink
// et pour écrire
website.fullLink = "https://codepen.io"
```

```javascript
const website = {
  protocol: "https",
  domain: "alyra.fr",
  get fullLink() {
    return `${this.protocol}://${this.domain}`
  },
  set fullLink(value) {
    const [protocol, domain] = value.split("://")
    this.protocol = protocol
    this.domain = domain
  },
}

/*
const website = {
  protocol: 'https',
  domain: 'alyra.fr',
  get fullLink() {
    return `${this.protocol}://${this.domain}`
  },
  set fullLink(value) {
    [this.protocol, this.domain] = value.split('://')
  }
};

*/

website.fullLink = "https://codepen.io"
```

https://codepen.io/alyra/pen/dyMyNXP

On peut aussi utiliser uniquement getter, au lieu de mettre en place la méthode id comme ceci:

```javascript
const alien = {
  name: "Deej",
  age: 410,
  id() {
    if (this.name) {
      return "_" + this.name.toLowerCase()
    }
  },
}
console.log(alien.id())
alien.id = "hahaha" // remplace id
```

On l'utilise avec `get`

```javascript
const alien = {
  name: "Deej",
  age: 410,
  get id() {
    if (this.name) {
      return "_" + this.name.toLowerCase()
    }
  },
}
console.log(alien.id())
alien.id = "hahaha" // ne fonctionne pas -> erreur
```

---

## Exercices

- [tour object methods](https://javascript-quizzes.netlify.app/object-methods)
- [Object - restaurant methods](https://codepen.io/alyra/pen/NWxXEbd) | [solution](https://codepen.io/alyra/pen/b8fc4c9f454bfebda41b4621d9283a13)
- [this](https://codepen.io/alyra/pen/xxVKVmN)
