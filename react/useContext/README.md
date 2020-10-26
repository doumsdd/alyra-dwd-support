# React Context API et `useContext` hook

Nous allons découvrir l’API Context de React en procédant à un refactoring. Notre point de départ est [ce repo GitHub](https://github.com/pehaa/alyra-gradients-context).
Nous allons retravailler l’application Alyra Gradients avec une approche alternative, en utilisant API Context. La structure de notre projet du départ est comme ceci :

```bash
src
├── App.js
├── App.test.js
├── components
│   ├── Footer.js
│   ├── Gradient
│   │   ├── GradientCode.js
│   │   ├── GradientPill.js
│   │   ├── GradientTagButton.js
│   │   ├── GradientTags.js
│   │   ├── GradientTitle.js
│   │   ├── gradient.css
│   │   └── index.js
│   ├── Gradients.js
│   ├── GradientsHeader.js
│   ├── GradientsList.js
│   └── GradientsSelect.js
├── gradients.js
├── index.css
├── index.js
├── serviceWorker.js
└── setupTests.js
```

![](https://wptemplates.pehaa.com/assets/alyra/diagram.png)

## Motivation

Regardons l'image ci-dessus. Nous utilisons `filter` et `setFilter` dans `GradientsSelect` et `GradientsTagButton`.

Leur common parent est le component `Gradients` et c'est là où nous trouverons le code :

```javascript
// src/components/Gradients.js
import React, { useState } from "react"
// ....

const Gradients = () => {
  const [filter, setFilter] = useState("all")
  // ...
}

export default Gradients
```

ensuite nous passons `filter` et `setFilter` en tant que props dans `GradientsSelect`.

Nous devons aussi poursuivre tout le chemin entre `Gradients` vers `GradientTagButton` en passant à chaque fois des props `filter` et `setFilter`.

Existe-il une autre possibilité ? Passer les props tout le long n'est pas très gênant dans ce projet-ci, mais imaginons un projet plus complexe...

Dans la programmation, le mot _context_ peut être interprété comme "l'information pertinente". On utilise _context_ dans React si une information est pertinente pour plusieurs components en même temps. Les exemples type sont : theme (_dark_ vs. _light_), language (version 'FR' ou 'EN'), le choix de devise dans une application e-commerce.

Voici un extrait de la documentation officielle de React

> Dans une application React typique, les données sont passées de haut en bas (du parent à l’enfant) via les props, mais cela peut devenir lourd pour certains types de props (ex. les préférences régionales, le thème de l’interface utilisateur) qui s’avèrent nécessaires pour de nombreux composants au sein d’une application. Le Contexte offre un moyen de partager des valeurs comme celles-ci entre des composants sans avoir à explicitement passer une prop à chaque niveau de l’arborescence.

> En utilisant le Contexte, nous pouvons éviter de passer les props à travers des éléments intermédiaires.

![](https://wptemplates.pehaa.com/assets/alyra/diagram-usecontext.png)

## Mise en place de context et son "provider"

```bash
mkdir src/context
touch src/context/FilterContext.js
```

```javascript
// src/context/FilterContext.js
import React, { useState, createContext } from "react"

// créer et exporter ("named") FilterContext object
export const FilterContext = createContext()

/* le component-provider qui embrassera la partie de notre app où on utilise ce context */

const FilterContextProvider = ({ children }) => {
  const [filter, setFilter] = useState("all")
  return (
    <FilterContext.Provider value={{ filter, setFilter }}>
      {children}
    </FilterContext.Provider>
  )
}

export default FilterContextProvider
```

Fichier `FilterContext.js` exporte `FilterContext` (named export) et `FilterContextProvider` (default export).

La props `value` de `Provider` permettra à tous ses components enfants d'avoir accès à la valeur passée. Les components enfant vont aussi se mettre à jour (re-render) quand `value` change.

Ici nous passons dans value un objet avec 2 clés : `filter` et `setFilter`.

## App

### App.js

Dans `App.js`, nous allons importer `FilterContextProvider` et le mettre en place.

```javascript
// src/App.js
import React from "react"
import Gradients from "./components/Gradients"
import GradientsHeader from "./components/GradientsHeader"
import Footer from "./components/Footer"
import FilterContextProvider from "./context/FilterContext"

function App() {
  return (
    <>
      <GradientsHeader>
        <h1 className="display-1">Alyra Gradients</h1>
        <p className="tagline">Ultime collection de plus beaux dégradés</p>
      </GradientsHeader>
      <main className="container">
        <h1 className="text-center my-4">Alyra Gradients</h1>
        <FilterContextProvider>
          <Gradients />
        </FilterContextProvider>
      </main>
      <Footer />
    </>
  )
}

export default App
```

### Gradients.js

Nous allons également modifier `Gradients.js`

```javascript
import React from "react"
import GradientsList from "./GradientsList"
import GradientsSelect from "./GradientsSelect"

const Gradients = () => {
  return (
    <>
      <GradientsSelect />
      <GradientsList />
    </>
  )
}

export default Gradients
```

![](https://wptemplates.pehaa.com/assets/alyra/diagram-usecontext.png)

## Consommer context avec `useContext`

`useContext` accepte un objet contexte (dans notre cas se sera `FilterContext`), et retourne la valeur actuelle du contexte. La valeur de `useContext(FilterContext)` est déterminée par la prop `value` du plus proche <FilterContext.Provider> au-dessus du composant dans l’arbre.

Quand le plus proche <FilterContext.Provider> au-dessus du composant est mis à jour, `useContext` déclenche un re-render avec la value la plus récente passée au fournisseur MyContext.

### GradientsList.js

```javascript
// src/components/GradientsList.js
import React, { useContext } from "react"
import { gradients } from "./../gradients"
import Gradient from "./Gradient"
import { FilterContext } from "./../context/FilterContext"

const GradientsList = (props) => {
  const { filter } = useContext(FilterContext)
  const list = gradients.filter((el) => {
    if (filter === "all") {
      return true
    }
    return el.tags.includes(filter)
  })
  return (
    <ul className="row list-unstyled">
      {list.map((el) => {
        const { name, start, end, tags = [] } = el
        return (
          <Gradient
            key={el.name}
            colorStart={start}
            colorEnd={end}
            name={name}
            tags={tags}
          />
        )
      })}
    </ul>
  )
}

export default GradientsList
```

## Gradient

Dans `Gradient` component nous allons enlever `filter` et `setFilter` en tant que props que nous passons ensuite vers `GradientTags`

## GradientTags

Dans `GradientTags` component nous allons enlever `filter` et `setFilter` en tant que props que nous passons ensuite vers `GradientTagButton`

## GradientTagButton

```javascript
// src/components/Gradient/GradientTagButton.js
import React, { useContext } from "react"
import { FilterContext } from "./../../context/FilterContext"

const GradientTagButton = ({ tag }) => {
  const { filter, setFilter } = useContext(FilterContext)
  const className = filter === tag ? "bg-light" : "bg-dark text-white"
  const handleTagClick = () => {
    setFilter(tag)
  }
  return (
    <button
      type="button"
      className={`btn btn-sm mr-2 ${className}`}
      disabled={filter === tag}
      onClick={handleTagClick}
    >
      {tag}
    </button>
  )
}

export default GradientTagButton
```

## GradientsSelect

```javascript
// src/components/GradientsSelect.js
import React, { useContext } from "react"
import { uniqueTags } from "../gradients"
import { FilterContext } from "./../context/FilterContext"

const GradientsSelect = () => {
  const { filter, setFilter } = useContext(FilterContext)
  const handleSelectChange = (e) => {
    setFilter(e.target.value)
  }
  return (
    <div className="input-group mb-3">
      <label className="input-group-text" htmlFor="select">
        Filtrer par tag
      </label>
      <select
        className="form-select"
        id="select"
        value={filter}
        onChange={handleSelectChange}
      >
        <option value="all">Tous</option>
        {tags.map((el) => (
          <option key={el} value={el}>
            {el}
          </option>
        ))}
      </select>
    </div>
  )
}

export default GradientsSelect
```

---

## Context recap :

- _contexte_ = information pertinente
- utile lorsque plusieurs components doivent partager la même information (thème, langue, devise)
- permettent d'éviter passer les props plusieurs niveaux plus bas
- Étapes de création :
  - créer le contexte `createContext`
  - créer le component `Provider` avec la props `value` que va tenir l'information pertinente
  - exporter le contexte et son provider
- Pour utiliser le contexte
  - Emballer vos components avec le provider
  - Dans les fichiers components, importer le contexte et passer le au hook `useContext`

---

## Exercices :

- [useContext - alyra gradients GradientsContext (todo)](https://github.com/pehaa/alyra-gradients-context-todo)
- [useContext - shopping + dark mode](https://github.com/pehaa/alyra-shopping-refactor-context)
