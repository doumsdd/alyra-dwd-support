# Projet Gradients

# Step 1 - create-react-app et configuration initiale

```bash
npx create-react-app react-alyra-gradients
```


### Installer Bootstrap5 et mettre en place Bootstrap5

```bash
yarn add bootstrap@next
```


### Head

Configurez la partie head :
  - title
  - lang
  - meta

remplacer les icônes et configurer `manifest.json`

### Structure du projet

Mettez en place un dossier `src/components` avec la structure comme ceci (structure recommendée, mais peut varier un peu ;))

```bash
src
├── App.js
├── App.test.js
├── components
│   ├── Footer.js
│   ├── Gradient
│   │   ├── GradientCode.js
│   │   ├── GradientPill.js
│   │   ├── GradientTitle.js
│   │   ├── gradient.css
│   │   └── index.js # (*)
│   ├── Gradients.js # (**)
│   ├── GradientsHeader.js
│   ├── GradientsList.js
│   └── GradientsSelect.js
├── gradients.js
├── index.css
├── index.js
├── serviceWorker.js
└── setupTests.js
```

(`*`) - contient le component Gradient  
(`**`) - component parent, contient GradientsList et GradientsSelect

### src/gradients.js

Ce fichier devrait exporter les variables `gradients` et `uniqueTags`

Vous pouvez utiliser [le contenu de ce fichier](https://codepen.io/alyra/pen/73e755888ff0a8fa07d0561d108537ac.js)


### src/components/GradientPill/gradient.css

Le fichier `src/components/Gradient/gradient.css` devrait contenir

```css
.card-gradient {
  width: 5rem;
  height: 5rem;
}
code {
  color: grey;
}
```

ce fichier devrait être importé dans `src/components/GradientPill.js`

### src/App.js

Mettez en place `GradiensHeader`, `Gradients` et `Footer` dans `src/App.js`

# Step 2 Migration depuis CodePen

Utilisez le code des exercices CodePen et migrez le tout dans votre app.

# Step 3 Working App

Mettez en place un component `GradientsSelect` avec le filtre par tag.

**Vous pouvez voir le site de référence [ici](https://alyra-gradients-bonus.netlify.app/)**

**DEADLINE : projet à rendre lundi 9h27**

# Bonus 

[ajouter des tags en tant que boutons](https://alyra-gradients-bonus.netlify.app/)

## Validation :

- rendu sur Github et déploiement sur Netlify
- bootstrap5 est installé avec yarn (utilisation de bootstrap depuis CDN n'est pas valide)
- title, lang, meta, favicons, manifest sont modifiées
- la structure est respectée
- le header avec le bouton est fonctionnel
- les dégradés sont affichés dans la page
- le select foncionne et permet de filter des dégradés par tag
- il n'y a pas de warning depuis la console dans VSCode
- [le html est valide (validator w3c)](https://validator.w3.org/nu/)
- remettre vos liens [ici](https://docs.google.com/spreadsheets/d/1aFirDN3S0Pgz0FFzXBNViLAo6YdbNFqhm-rLe-iN5aw/edit#gid=464596968)

