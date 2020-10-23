# React Google Fonts Widget

![](https://assets.codepen.io/4515922/pangramme_1.jpg)

Vous trouverez ici le modèle à reproduire [alyra-google-fonts-widget.](https://alyra-google-fonts-widget.netlify.app/)

Votre applications utilise [**Developer API de Google Fonts**](https://developers.google.com/fonts/docs/developer_api) afin d'afficher :

- 10 polices les plus récentes
- 10 polices les plus _trending_
- 10 polices les plus populaires

<hr />
 
 **Chaque de polices** est affichée avec des détails :
 
   - son nom 
   - nombre de variants
   - catégorie (serif, sans-serif, ...)
   - l'apperçu 
   - le lien vers la police sur [fonts.google.com](https://fonts.google.com)
   
<hr />

**L'apperçu** contient un texte (initialement un [pangramme](https://fr.wikipedia.org/wiki/Pangramme), par exemple _Portez ce whisky au vieux juge blond qui fume._) Ce texte peut être modifié par utilisateur.

Le texte d'apperçu est affiché avec la propriété _font-family_ égale à la police en question.

L'utilisateur peut également modifier la taille d'affichage (entre 8px et 48px).

<hr />

**Le lien vers la page de police sur fonts.google.fonts** - attention aux polices dont le nom est composé des plusieurs mots,
par exemple le lien pour Kumbh Sans est https://fonts.google.com/specimen/Kumbh+Sans (il contient le symbole `+` entre chaque mot)

<hr />

Afin d'afficher des apperçus, voud devez charger les polices google en question.

Il existe quelques solution pour charger des polices google dynamiquement, par exemple [react-google-font-loader](https://github.com/jakewtaylor/react-google-font-loader)

<hr />

La mise en page peut être modifiée, elle n'est pas imposée. Tâchez à avoir votre HTML valide et réfléchissez sur l'experience utilisateur.

## Validation :

- rendu sur GitHub et déploiement sur Netlify
- title, lang, meta, favicons, manifest sont modifiées
- utilisation d'API Google Fonts
- police est affichée correctement (tous les éléments démandé)
- les polices affichées sont chargées
- texte est "modifiable"
- taille de polices est modifiable
- pas de warning depuis la console dans VSCode ni dans navigateur
- html est valide (validator w3c)
