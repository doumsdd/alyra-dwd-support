JavaScript est synchronique. Le script est executé du haut en bas, une chose à la fois.

Ceci n'est pas toujours suffisant. Imaginons que notre script a besoin des informations qui arrivent avec certain délai, et en plus la durée de ce délai n'est pas connue.

JavaScript a l'objet `Promise` pour réaliser des traitements de façon asynchrone. Nous allons besoir d'utiliser cette approche pour recupérer des données via une requete HTTP.

Comment ça fonctionne ? Que pouvons nous faire avec une "promise" ?

Nous pouvons, dans notre code, planifier ce qui devrait se passer au moment où la promesse sera tenue et nous récevrons les données.

Et ce code _"planning"_ sera executé au moment où cela se produira.

```javascript
promiseMadeToMe
  .then((result) => {
    /* ici je planifie ce que je fais si la promesse est tenue et je reçois result
     */
  })
  .catch((error) => {
    // ce code executera si jamais il y aura une erreur
    // console.log(error.message)
  })
```

Imaginons maintenant que nous voulons créer une application météo, nous allons profiter des données disponibles avec l'API de OpenWeather.

Afin d'obtenir une promesse nous allons utiliser la fonction JavaScript `fetch`

`fetch(wheatherAPIUrl)` <- ceci est une promise, `fetch` retourne une promesse

```javascript
fetch(url)
  .then((result) => {
    if (result.ok) {
      return result.json() // then retourne une promise
    } else {
      throw new Error(result.statusText)
    }
  })
  .then((result) => {
    console.log(result) // enfin !!
  })
  .catch((error) => {
    console.log(error.message)
  })
```

**CSS-Tricks Blog**
https://codepen.io/alyra/pen/QWNBbRj

**StarWars API**
https://codepen.io/alyra/pen/VwaBvqZ
