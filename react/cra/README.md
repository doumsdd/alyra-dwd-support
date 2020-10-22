# CRA

[Create React App (ou CRA)](https://create-react-app.dev/) est un starter pour des applications React, officiellement recommandé et maintenu par l'équipe de React.

## Pourquoi ?

- CRA configure tous les outils de développement de l'application, en particulier :
  - webpack (bundler des fichier)
  - babel (compilateur)
  - prettier (pour formater votre code)
  - linter (pour détecter des erreurs)
- CRA lance un serveur de développement en mode *hot reload* (pas besoin de rafraîchir le navigateur)
- CRA permet de générer la version optimisée pour la *production*

## cra + bootstrap5 step by step

Dans la partie suivante, nous allons voir comment nous pouvons démarrer un projet avec CRA et bootstrap 5.

### Step 0 - installer une nouvelle app

```bash
npx create-react-app nom-de-mon-app
cd nom-de-mon-app
code .
```

Dans les lignes ci-dessus on :

 - installe une nouvelle application React, dans un répertoire `nom-de-mon-app`
 - on se déplace dans ce répertoire
 - on lance VSCode
 
### Step 1 - VSCode
 
 Ouvrir le Terminal dans VSCode et lancer app en mode dévéloppement
 
```bash
yarn start
```

ou avec `npm`

```bash
npm start
``` 

L'appli est lancée, elle "hot-reload" sous l'addresse http://localhost:3000 (le numéro du port peut varier)

Pour arrêter le serveur `Ctrl+C` et pour relancer `yarn start`.

### Step 2 - bootstrap (si besoin)

Nous allons intaller bootstrap5 dans le projet 

```bash
yarn add bootstrap@next
``` 

Suite à l'installation `bootstrap` sera ajouter dans le dossier `node_modules`
Un peu plus tard, nous allons profiter du fichier complet de bootstrap qui se trouve dans `node_modules/bootstrap/dist/css/bootstrap.css`

### Architecture initiale du projet

```bash
├── README.md
├── node_modules
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html  #<div id="root"></div> est ici !
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
├── src
│   ├── App.css
│   ├── App.js  #component <App /> est ici !!
│   ├── App.test.js
│   ├── index.css
│   ├── index.js  #ReactDOM.render(<App/ >, document.getElementById("root") se passe ici
│   ├── logo.svg
│   ├── serviceWorker.js
│   └── setupTests.js
└── yarn.lock
```

### public/index.html

Passage obligatoire pour mettre à jour la partie `head` de l'appli (lang, title, meta, favicons, apple-touch-icon)

A l'occasion on met à jour le ficher `public/manifest.json`

### src/index.js

Ici, on peut mettre en place le fichier CSS principale 

```javascript
import React from "react"
import ReactDOM from "react-dom"
import "bootstrap/dist/css/bootstrap.css" // <- importer bootstap, depuis node_modules
import "./index.css" // <- supprimer le contenu par défaut de ce fichier
import App from "./App"
import * as serviceWorker from "./serviceWorker"

// le reste sans changement
```

### Components

Pour mieux organiser notre projet, nous allons créer un dossier components dans le repertoire `src`.
Tous nos components seront créer dans repertoire.

```bash
mkdir src/components
```

Voici comment nous allons mettre en place nos components :

```bash
touch src/components/MonComponent1.js
```

```bash
src
├── App.js
├── App.test.js
├── components
│   ├── MonComponent1.js
│   ├── MonComponent2.js
│   └── MonComponent3.js
├── index.css
├── index.js
├── serviceWorker.js
└── setupTests.js
```

Attention: `MonComponent1` est un très mauvais nom pour un component, nommez vos components selons leurs rôles dans l'application.

#### Component-Starter

Voici un petit starter qui vous permettera de démarrer avec n'importe quel component :

```javascript
// src/components/MonComponent1.js
import React from 'react'

const MonComponent1 = () => {
  return null
}

export default MonComponent1
```

### App

Voici l'exemple comment importer un component dans `src/App.js`

```javascript
// src/App.js
import React from "react"
import MonComponent1 from "./components/MonComponent1"

function App() {
  return (
    <div className="container my-3">
      <header className="App-header">
        <h1>Mon titre</h1>
      </header>
      <MonComponent1 />
    </div>
  )
}

export default App
```