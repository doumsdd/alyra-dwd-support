**HTML** _HyperText Markup Language_ est un langage de balises permettant :

- de structurer le contenu
- d'avoir de l'hypertexte dans un navigateur web.

Il coexiste avec deux autres technologies Web :

- **CSS** pour décrire la présentation visuelle
- **JavaScript** pour des fonctionnalités interactives

## Structure

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Metadonnées du document -->
  </head>
  <body>
    <!-- Contenu du document -->
  </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <title>Mon Document</title>
    <meta charset="utf-8" />
    <!-- Document metadata -->
  </head>
  <body class="full light">
    <header id="top">
      <h1>Bienvenue</h1>
    </header>
    <main>
      <!-- ... contenu principal ... -->
    </main>
    <footer>
      <a href="#top">Retour vers le haut</a>
    </footer>
  </body>
</html>
```

![rangement ikea](https://s3-us-west-2.amazonaws.com/s.cdpn.io/4515922/wardrobe.jpg)

###Métaphore
Un rangement Ikea (html) = la notice qui permet de l'assembler ([head](https://developer.mozilla.org/fr/docs/Web/HTML/Element/head)) + le rangement lui-même ([body](https://developer.mozilla.org/fr/docs/Web/HTML/Element/body))

<a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/4515922/removehead.mp4" target="_blank" rel="noreferrer noopener">Voici ce qui se passe quand on enlève la partie head.</a>

## Syntaxe d'une balise HTML

```html
<nomdebalise>contenu de l'élément</nomdebalise>

<!-- éléments html peuvent avoir des attributs  -->

<nomdebalise attribut1="sa valeur" attribut2="valeur"
  >contenu de l'élément</nomdebalise
>

<!-- Il y a aussi des balises autofermantes (qui ne possèdent pas du contenu mais uniquement des attributs -->

<nomdebalise attribut1="sa valeur" attribut2="valeur" />

<!-- ceci aussi est correcte -->

<nomdebalise attribut1="sa valeur" attribut2="valeur"></nomdebalise>
```

A en lire aussi [ici](https://developer.mozilla.org/fr/docs/Apprendre/Commencer_avec_le_web/Les_bases_HTML) - lecture obligatoire !

## Balises HTML

Ci-dessous vous trouverez les principales balises HTML **classées par le contexte d'utilisation.**

Attention: Cette liste n'est pas 100% complète. Dans un objectif de clarté, certaines balises rarement utilisées, obsoletes ou "experimentales" ne sont pas inclues.

### Racine principale (root)

`html`

### Métadonnées du document

`head`  
` base``link `  
`style`
`title`
`meta`

### Racine de sectionnement

`body`

### Sectionnement du contenu

**Objectif** : donner une structure logique au document !

`main`  
`section`  
`article`  
`header`  
`h1, ... h6`  
`footer`  
`aside`  
`nav`

### Organisation du contenu textuel

**Objectif** : identifier le sens du contenu !

`p`  
`blockquote`  
`ul` `ol` `li`
`dl` `dt` `dd`  
`figure` `figcaption`  
`pre`  
`main`  
`div`

### Organisation des fragments au sein d'une ligne de texte

**Objectif** : identifier la signification ou la mise en forme

`a`  
`strong` `b`  
`em` `i`  
`br`  
`code`  
`small`  
`span`  
`sub` `sup` (par exemple : H<sub>2</sub>O et m<sup>3</sup>)
`time`  
`del` `ins` (par exemple : Cette formation durera <del>5 mois</del> <ins>6 mois</ins>.

### Images, Multimedia et Embedded Content

**Objectif** : afficher les images et multimedia, intégrer le contenu _externe_
`img`  
`picture`  
`source`  
`audio`
`video`  
`track`  
`iframe`

### Scripts

**Objectif** : Gérer l'execution des scripts

`canvas`  
`script` et `noscript`

```html
<script>
  alert("Hello JavaScript Lovers!")
</script>
<noscript
  >Pour recevoir nos salutations, veillez activer JavaScript dans votre
  navigatuer :)</noscript
>
```

Vous pouvez voir le code ci-dessus en action en cliquant [ce lien](https://cdpn.io/alyra/debug/1a70873c7b9713e08a6d00b45ee1b0ab) et ensuite en désactivant JavaScript dans votre navigateur et en réchargant la page.

### Tables

**Objectif** : Mettre le contenu dans les cases 😉

`table`  
`thead` `tbody` `tfoot`  
`tr` `td` `th`  
`colgroup` `col`

### Formulaires

**Objectif** : Envoyer des données !!!

`form`
`fieldset` `legend`  
`label`  
`button`  
`input`  
`select` `optgroup` `option`
`progress`  
`textarea`

### Éléments interacifs

`details` `summary`

### Éléments obsoletes

**Attention** - évitez à les utiliser

`acronym`
`applet`
`basefont`
`bgsound`
`big`
`blink`
`center`
`command`
`content`
`dir`
`element`
`font`
`frame`
`frameset`
`image`
`isindex`
`keygen`
`listing`
`marquee`
`menuitem`
`multicol`
`nextid`
`nobr`
`noembed`
`noframes`
`plaintext`
`shadow`
`spacer`
`strike`
`tt`
`xmp`

## Catégories de contenu

Chaque élément HTML est membre d'un certain nombre de catégories de contenu (par exemple _phrasing content_ ou _interactive content_). Il y a plusieurs règles qui sont basés sur ce classement.

### Phrasing content (contenu phrasé)

`a` (s'il contient lui-même _phrasing content_)  
 `abbr` `audio` `b` `bdo` `br` `button` `canvas` `cite` `code` `command` `data` `datalist` `dfn` `em` `embed` `i` `iframe` `img` `input` `kbd` `keygen` `label` `mark` `math` `meter` `noscript` `object` `output` `picture` `progress` `q` `ruby` `samp` `script` `select` `small` `span` `strong` `sub` `sup` `svg` `textarea` `time` `var` `video` `wbr` et texte.

`p` - contenu autorisé : contenu phrasé

```html
<!-- ceci est correct (et vrai) -->
<p>Ca se complique, hein ? Ne vous inquietez pas, on va continuer doucement en veillant que vous appreniez de bonnes pratiques.</p>

<!-- ceci n'est pas correct (et faux) -->
<p><div>Pfff, c'est trop compliqué.</div></p>
```

Regardons ensemble, le code dans le pen suivant. Pourquoi le texte n'est pas écrit en rouge tomate ??? 🤔

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="html,result" data-user="alyra" data-slug-hash="QWjJzRB" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Qu'est qui va pas ici ? ">
  <span>See the Pen <a href="https://codepen.io/alyra/pen/QWjJzRB">
  Qu'est qui va pas ici ? </a> by Alyra (<a href="https://codepen.io/alyra">@alyra</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<!---
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
-->

**Comment savoir ?**

- Suivre la spécifation - [MDN - Référence des éléments HTML](https://developer.mozilla.org/fr/docs/Web/HTML/Element)
- Veiller à toujours valider son document HTML

### Ressources

- [MDN - Référence des éléments HTML](https://developer.mozilla.org/fr/docs/Web/HTML/Element)
- [HTML Reference](https://htmlreference.io/)

---

## Exercices

- [Sac de voyage](https://codepen.io/alyra/pen/yLYxEpJ) | [solution](https://codepen.io/alyra/pen/50e0ae1bd5d18d37e3f239c6d673c1d1)
- [Trottinette](https://codepen.io/alyra/pen/vYNzrav) | [solution](https://codepen.io/alyra/pen/03cdc8f33f5523d04ba8ac8c9c5a615b)
- [Personnages Starwars](https://codepen.io/alyra/pen/QWjPjMz) | [solution](https://codepen.io/alyra/pen/aab636e7598ee96a853e589048316ed0)
