# JSX - 2

# Expressions JavaScript

JSX permet de faire un mixte de la structure HTML et des expressions JavaScript. Expressions JavaScript sont intégrées entre des accolades (ceci ressemble un peu aux *template literals*)

JSX est aussi une expression JavaScript.

```javascript
const element = <p>Vous avez {10 + 1} notifications.</p>
// HTML <p>Vous avez 11 notifications.</p>
```

```javascript
const lang = "en"
const element = <h1 lang={lang}>{lang === "en" ? 'Hello World!' : 'Bonjour le Monde !'}</h1>
// HTML <h1 lang="en">Hello World!</h1>
```

```javascript
function capitalize(string) {
  return string[0].toUpperCase() + string.slice(1).toLowerCase();
}
const name = "paulIna"
const element = <h1>Hello {capitalize(name)}</h1>
// <h1>Hello Paulina</h1>
```

On peut alors intégrer une expression JavaScript, mais attention - ceci ne veut pas dire qu'on peut écrire n'importe quel code js entre les accolades. Ceci doit être une expression - un code qui donne une valeur en tant que le résultat.

Exemples valides :  

```javascript
<div id={myVariable}>
  <h2>{array.length ? 'Les résultats :' : 'Pas de résultats'}</h2>
  <p>{2**16}</p>
  <p>{myFunction()}</p>  
</div>
```

Exemples **pas valides** :  

```javascript
<div id={const myVariable = 'top'}>
  <h2>{if (array.length) {Les résultats :'} else {'Pas de résultats'}}</h2>
</div>
```

Autrement dit, une expression est un bout de code qui pourrait se trouver à droite d'un symbole `=`.

**Attention** aux apostrophes, si on les aujoute autour des accolades, celles-ci sont interpretées en tant que `string` : 

```javascript
const element = <h1 lang="{lang}">Hello World!</h1>`

// HTML -> <h1 lang="{lang}">Hello World!</h1>
```

# Espaces vides

```javascript
const element = (
  <p>
    Les composants vous permettent de découper l’interface utilisateur en
    éléments indépendants et réutilisables,{" "}
    <strong>
      vous permettant ainsi de considérer chaque élément de manière isolée
    </strong>
  </p>
);
```

Cette espace vides `{" "}` vient d'être ajoutée par Prettier quand j'ai sauvegardé le code 

```javascript
const element = (
  <p>
    Les composants vous permettent de découper l’interface utilisateur en
    éléments indépendants et réutilisables, <strong>
      vous permettant ainsi de considérer chaque élément de manière isolée
    </strong>
  </p>
);
```

On peu voir le rendu [sans `{" "}` ici.](https://codepen.io/alyra/pen/OJNxRJV) 

![](https://assets.codepen.io/4515922/spaces.png)

JSX supprime les espaces en début et en fin de ligne. Il supprime également les lignes vides. Les sauts de lignes adjacents aux balises sont retirés.

# Boolean expressions et conditional rendering

Les expressions boléennes, ainsi que `undefined` et `null` ne génére pas de rendu :

```javascript
const age = 10
const element = <span>{age >= 10}</span>
// <span></span>
```

## &&

Les expressions boléennes peuvent être utilisées afin d'afficher un rendu selon une condition :

```javascript
const name = "Alyra"
const element = (
  <header>
    <h1>Bienvenue</h1>
    {name.length > 0 && <p>Notre école s'appelle {name}</p>}
    { /* !!name && <p>Notre école s'appelle {name}</p> */ }
  </header>
)
```


```javascript
const alien =  {
  age: 100,
  name: "Deej"
}
const element = (
  <section>
    <h2>Bienvenu {alien.name} !</h2>
    {alien.age >= 100 && <button>Partez en mission</button>}
  </section>
)
/* 
<section>
  <h2>Bienvenu Deej !</h1>
  <button>Partez en mission</button>
</section>
*/
```

## conditions ternaires

```javascript
const lang = "en"
const element = <h1 lang={lang}>{lang === "fr" ? 'Bienvenue' : 'Welcome'}</h1>
```

```javascript
const shoppingList = ["Miel", "Sel", "Cumin"]
const length = shoppingList.length
const element = (
  <section>
    <h2>Shopping List</h2>
    {length 
      ? <p>Vous avez {length} articles à acheter</p>
      : <p>Avez-vous besoin de quelque-chose ?</p>
    }
  </section>
)
```

# Props spread

```
const props = {
  lang: "en",
  id: "top",
  className: "display-1"
}
const element = <h1 {...props}>Hello World</h1>
```

```
const props = {
  lang: "en",
  id: "top",
  className: "display-1"
}
const element = <h1 className="display-4" {...props} lang="fr">Bonjour le Monde</h1>

/* 
React.createElement(
  "h1",
  Object.assign({className: "display-4"}, props, { lang: "fr" }},
  Bonjour le Monde
)
React.createElement(
  "h1",
  Object.assign({className: "display-4"}, {lang: "en", id: "top", className: "display-1"}, { lang: "fr" }),
  Bonjour le Monde
)
React.createElement(
  "h1",
  {className: "display-1", lang: "fr", id: "top"},
  Bonjour le Monde
)
*/
// HTML <h1 class="display-1" lang="fr" id="top">Bonjour le Monde</h1>
```

# Arrays

```javascript
const shoppingList = ["miel", "sucre", "cumin", "curry"];

/* const element = (
  <ul>
    {[
      <li>miel</li>,
      <li>sucre</li>,
      <li>cumin</li>,
      <li>curry</li>
     ]}
  </ul>
);*/

const element = (
  <ul>
    {shoppingList.map((el) => (
      <li key={el}>{el}</li>
    ))}
  </ul>
);
```

```javascript
const definitions = [
  {term: 'React', description: 'une librarie JavaScript'},
  {term: 'JSX', description: 'une extension syntaxique de JavaScript'},
  {term: 'Gatsby', description: 'un framework basé sur React'} 
];

const element = (
  <dl>
    {definitions.map((el) => {
      return (
        <React.Fragment key={el.term}>
          <dt>{el.term}</dt>
          <dd>{el.description}</dd>
        </React.Fragment>
      );
    })}
  </dl>
);
```

[[[pen slug-hash='MWyvGRZ' height='300' theme-id='1']]]

---

## Exercices

  - [JSX expression - hello](https://codepen.io/alyra/pen/qBZXEje) | [solution](https://codepen.io/alyra/pen/3e7e235fbb4c229a14585e3b8ef867df)
 - [JSX - espressions - logged-in](https://codepen.io/alyra/pen/RwaZNaW) | [solution](https://codepen.io/alyra/pen/43004448ad3a73d223d7f1c1eb6598e7)
 - [JSX - espressions - notifications](https://codepen.io/alyra/pen/poyrvEa) | [solution](https://codepen.io/alyra/pen/bc89eb35101c603941bdae0a9b881dfb)
 - [JSX - espressions - notifications 1](https://codepen.io/alyra/pen/JjXyxjo) | [solution](https://codepen.io/alyra/pen/bdf636434aa83dde7e1e159b4e78dccc)
 - [JSX - notifications list](https://codepen.io/alyra/pen/YzqxMEP) | [solution](https://codepen.io/alyra/pen/f7801accec0de64a8473089fd051f25d)
 - [JSX - notifications title + list](https://codepen.io/alyra/pen/bGprJaW) | [solution](https://codepen.io/alyra/pen/10413263fabe4668bf815a7d2ad05ec8)
 - [JSX button](https://codepen.io/alyra/pen/YzqxoQO) | [solution](https://codepen.io/alyra/pen/d90868a92c92e2736befa9685f38a1e4)
 - [JSX title](https://codepen.io/alyra/pen/VwaMbMP) | [solution](https://codepen.io/alyra/pen/d90868a92c92e2736befa9685f38a1e4)
 - [JSX smoothie](https://codepen.io/alyra/pen/xxVXdWZ) | [solution](https://codepen.io/alyra/pen/40a70e8ed7e387d45c8a2581e15efc4d)









