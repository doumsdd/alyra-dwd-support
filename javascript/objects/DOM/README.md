# DOM - Document Object Model

Document Object Model, (DOM), est une représentation objet du document HTML. Quand nous utilisons JavaScript dans le navigateur nous avons accès à l'objet `document`. 
Cet objet contient la structure de notre document HTML, nous permet de la modifier et gérer des interactions. Nous allons analyser ses propriétés et méthodes les plus importantes.

```javascript
console.dir(document)
```

## Sélectionner un élément : 

### document.documentElement

`document.documentElement` nous donne accès à l'élément `html` de notre document.
```javascript
console.dir(document.documentElement)
```

```javascript
document.documentElement // correspond au html
document.documentElement.lang // 'fr'
```

### document.body

`document.body` nous donne accès à l'élément `body` de notre document.

```javascript
document.body.style.background = "red"
```

### document.getElementById()

`document.getElementById('id-name')` nous donne accès à l'élément avec l'attribut id `id-name`.  `document.getElementById('id-name')` retourne l'élément s'il existe ou `null.`

On peut avoir le même résultat avec la méthode plus générique `document.querySelector()`, comparons ces 2 méthodes
```javascript
document.getElementById('id-name')
document.querySelector('#id-name') // comme dans les sélecteurs CSS
```

`getElementById()` s'applique uniquement sur `document`

```javascript
document.getElementById("cookie-info").remove()
document.getElementById("#pub").remove()
```

### document.querySelector(), element.querySelector()

Utilise les même sélecteurs que css.  
Trouve un élément, premier que correspond au sélecteur.

```javascript
const cookie = document.querySelector("#cookie-info")
cookie.querySelector("span").remove()
```

On aura le même résultat pour `document.querySelector('#id-name')` et  `document.getElementById('id-name')`.

### document.querySelectorAll('selector')

Le résultat retourné est une `NodeList`, une structure semblable à l'array.
Si aucun élément ne correspond pas au sélecteur, le résultat est une liste vide `[]`
On peut parcourir  `document.querySelectorAll('selector')` avec 
  - la boucle `for ... of`, 
  - la méthode `.forEach()` 
  - avec la boucle for classique

```javascript
const allButtons = document.querySelectorAll("button")
for (let button of allButtons) {
  button.disabled = true
}
```

```javascript
const allButtons = document.querySelectorAll("button")
allButtons.forEach((button) => {
  button.disabled = true
})
```

### document.getElementsByTagName('tag')

```javascript
const allParagraphs = document.getElementsByTagName("p")
```

### document.getElementsByClassName('.class-name')

```javascript
const allParagraphs = document.getElementsByClassName(".hidden")
```

## Des attributes

### Les attributes `standard`

Les attributes HTML `standard` peuvent être utilisés  "directement" en tant que une propriété d'un élément

```javascript
// attribut lang
document.documentElement.lang
const el = document.querySelector("p")
// attribut id
el.id
```

## class

Au lieu de propriété `class` nous avons `className` et `classList`

```html
<body class="bg-dark container"></body>
```

```javascript
document.body.class // undefined
document.body.className // "bg-dark container"
document.body.classList.length // 2
document.body.classList.contains("bg-dark") // true
document.body.classList.add("text-white")
document.body.classList.remove("container")
```

[Plus d'information ici - MDN](https://developer.mozilla.org/fr/docs/Web/API/Element/classList)

## non-standard attributes

Pour non-standard attributs (les attributs crées par l'utilisateur) nous devons utiliser les méthodes `hasAttribute(), setAttribute(), getAttribute(), removeAttribute()`.
Ces méthodes fonctionnent aussi pour des attributs standard.

```html
<body author="Franck"></body>
```

```javascript
document.body.hasAttribute("author") // true
document.body.author // undefined
document.body.getAttribute("author") // 'Franck'
document.body.setAttribute("author", "Paulina")
document.body.getAttribute("author") // 'Paulina'
document.body.removeAttribute("author")
```

Attention, ceci n'est pas une bonne pratique. Les attributs personnalisés devraient commencer par `data-`. En plus, si nous respectons cette règle, nous pouvons les accéder via la propriété `dataset`.

```html
<body data-author="Franck"></body>
```

```javascript
document.body.hasAttribute("data-author") // true
document.body["data-author"] // undefined
document.body.dataset.author // 'Franck'
document.body.dataset.author = "Maxime"
document.body.getAttribute("data-author") // 'Maxime'
document.body.setAttribute("data-author", "Paulina")
document.body.getAttribute("data-author") // 'Paulina'
document.body.removeAttribute("data-author")
// ou
delete document.body.dataset.author
```

## Modification du document

### element.textContent

Nous pouvons modifier le contenu textuel au sein de notre document HTML.

```javascript
const tagline = document.querySelector("#tagline")
const hellos = ["Salut", "Hello", "Cześć", "Hola"]
const randomHelloIndex = Math.floor(Math.random() * hellos.length)
tagline.textContent = hellos[randomHelloIndex]
```

### element.innerHTML

```javascript
const tagline = document.querySelector("#tagline")
const hellos = ["Salut", "Hello", "Cześć", "Hola"]
const randomHelloIndex = Math.floor(Math.random() * hellos.length)
tagline.innerHTML = `<strong>${hellos[randomHelloIndex]}</strong>`
```

### document.createElement(), before, after, prepend/append

```javascript
const 'cookieInfo' = document.createElement("p")
p.textContent = "Ce site n'utilise pas des cookies."
document.body.append(cookieInfo)
```

![](https://wptemplates.pehaa.com/assets/alyra/prepend-append.png)

https://codepen.io/alyra/pen/GRoLXBj

### insertAdjacentHTML

```javascript
const 'cookieInfo' = `<p>Ce site n'utilise pas des cookies.</p>`
document.body.insertAdjacentHTML('afterend', cookieInfo)
```

![](https://wptemplates.pehaa.com/assets/alyra/insertadjacent.png)

https://codepen.io/alyra/pen/ZEQZMqq

### element.addEventListener

`el.addEventListener(event, handleEvent)`

`handleEvent` est une fonction callback

```javascript
const myButton = document.querySelector("#my-button")
const handleButtonClick = (event) => {
  alert("button clicked !!!")
  console.log(event)
}
myButton.addEventListener("click", handleButtonClick)
```

On peut profiter de l'interactivité des éléments de formulaires. On peut les utiliser en dehors d'élément `form`. Les types d'event que nous allons utiliser souvent sont `input` et `select` et `change`.

https://codepen.io/alyra/pen/LYGoobE

```html
<label for="mode">Mode sombre</label>
  <input type="checkbox" id="mode">
</label>
```

```javascript
const modeInput = document.getElementById("mode")
modeInput.addEventListener("change", function (event) {
  if (modeInput.checked) {
    // if (this.checked)
    // if (event.currentTarget.checked)
    // if (event.target.checked)
    alert("Mode sombre")
  } else {
    alert("Mode claire")
  }
})
```

```javascript
const modeInput = document.getElementById("mode")
modeInput.addEventListener("change", () => {
  document.body.classList.toggle("bg-dark")
  document.body.classList.toggle("text-white")
})
```

https://codepen.io/alyra/pen/vYLwyJx

[Bonus - exemple avec localStorage](https://codepen.io/alyra/pen/wvMZVqo)

---

## Exercices

- [Dom - top5](https://codepen.io/alyra/pen/dyGLgoX) | [solution](https://codepen.io/alyra/pen/20c665db9b2bf35ce56635b71b37e5bd)
- [Dom - top5 + attributs](https://codepen.io/alyra/pen/dyGLgpp) | [solution](https://codepen.io/alyra/pen/2dcf464398e04c4a07a2fab6d80b8df8)
- [Dom - top5 + attributs](https://codepen.io/alyra/pen/jOWReMe) | [solution](https://codepen.io/alyra/pen/1e6aaae79019f03cbde8b95bc7432e13)
- [Lorem Ipsum](https://codepen.io/alyra/pen/mdVYMje) | [solution](https://codepen.io/alyra/pen/556c09a96bbc23c76c05760805f18a3d)
- [Dom veilles 1](https://codepen.io/alyra/pen/XWXwaeY) | [solution](https://codepen.io/alyra/pen/663748fcb0a8c328ad24d8b996e29392)
- [Dom veilles 2](https://codepen.io/alyra/pen/abdryWa) | [solution](https://codepen.io/alyra/pen/b4bb65ef7816f7675cb3629dee091c2d)
- [Date du jour](https://codepen.io/alyra/pen/mdVYMpJ) | [solution](https://codepen.io/alyra/pen/23049d07c690bcc660a40cbbf751ac7e)
