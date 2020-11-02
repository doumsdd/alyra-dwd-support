# Promise, fetch et useEffect

## Promise

JavaScript est synchrone. Le script est executé du haut en bas, une chose à la fois.

Ceci n'est pas toujours suffisant. Imaginons que notre script a besoin des informations qui arrivent avec certain délai, et en plus la durée de ce délai n'est pas connue.

JavaScript a l'objet `Promise` pour réaliser des traitements de façon asynchrone. Nous allons utiliser cette approche pour recupérer des données via une requete HTTP.

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
    // ce code executera si jamais il y avait une erreur
    // console.log(error.message)
  })
```

## Promises & fetch

Imaginons maintenant que nous voulons créer une application météo, nous allons profiter des données disponibles avec l'API de OpenWeather.

Afin d'obtenir une promesse nous allons utiliser la fonction JavaScript `fetch`, `fetch(wheatherAPIUrl)` retourne est une promise.

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

## Promises & fetch avec React - useEffect

Nous allons maintenant analyser 2 exemples où nous récuperons des données de la façon asynchrone via une API et les afficher dans le component React.

**CSS-Tricks Blog**

Dans cet exemple, nous allons afficher 10 derniers articles publiés sur le blog [CSS-Tricks](https://css-tricks.com). Nous allons les récuperer avec l'API rest de WordPress (CSS-Tricks est fait avec WordPress) - https://css-tricks.com/wp-json/wp/v2/posts


Nous allons mettre en place une variable de state `posts`, avec la valeur initiale `[]`. Nous allons recuperer les posts avec la méthode `fetch`. Ceci devrait se passer au moment où notre componenent `Blog` monte. Pour cela nous allons utiliser le hook `useEffect` avec , `[]` en tant que son deuxième paramètre.


```javascript
const Blog = () => {
  const [posts, setPosts] = React.useState([]);
  React.useEffect(() => {
    fetch("https://css-tricks.com/wp-json/wp/v2/posts")
      .then((response) => {
        if (response.ok) {
          return response.json();
        }
        throw new Error("quelque chose n'a pas marché");
      })
      .then((result) => {
        console.log(result);
        setPosts(result);
      })
      .catch((error) => {
        console.log(error.message);
      });
  }, []);

  return (
    <section className="container">
    </section>
  );
};
```

Nous allons étudier la structure des données retournées par `response.json()`

![](https://wptemplates.pehaa.com/assets/alyra/css-tricks-data.png)

et ensuite mettre les en place dans notre `<section className="container"></section>` :


```javascript
const Blog = () => {
  const [posts, setPosts] = React.useState([]);
  React.useEffect(() => {
    fetch("https://css-tricks.com/wp-json/wp/v2/posts")
      .then((response) => {
        if (response.ok) {
          return response.json();
        }
        throw new Error("quelque chose n'a pas marcher");
      })
      .then((result) => {
        console.log(result);
        setPosts(result);
      })
      .catch((error) => {
        console.log(error.message);
      });
  }, []);

  return (
    <section className="container">
      <h1>Derniers Articles de CSS-Tricks</h1>
      {posts.map((post) => {
        return (
          <article key={post.id}>
            <h2
              className="h5"
              dangerouslySetInnerHTML={{
                __html: DOMPurify.sanitize(post.title.rendered)
              }}
            />
            <div
              dangerouslySetInnerHTML={{
                __html: DOMPurify.sanitize(post.excerpt.rendered)
              }}
            />
          </article>
        );
      })}
    </section>
  );
};
```


https://codepen.io/alyra/pen/QWNBbRj

**StarWars API**

Dans le deuxième exemple nous allons jouer avec l'api Star Wars et afficher la liste des planètes avec l'information sur leurs populations.

L'url qui nous permet d'afficher les planètes est `https://swapi.dev/api/planets/?page=${page}`, le paramètre `page` permet d'afficher des planètes par dizaine, `page=3` affiche 3e dizaine des planètes.


https://codepen.io/alyra/pen/KKMRGrB
