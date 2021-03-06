# HTML - Introduction

**HTML** _HyperText Markup Language_ est un langage de balises permettant :

- de représenter le contenu d'une page web et de le structurer
- d'avoir de l'hypertexte dans un navigateur web.

Il coexiste avec deux autres technologies Web :

- **CSS** pour décrire la présentation visuelle
- **JavaScript** pour des fonctionnalités interactives

HTML utilise des **balises** (en anglais *tags*) qui sont insérées au sein d'un texte. Par exemple, chaque paragraphe est encadré par une balise paragraphe (`p`). Le titre principale sera encadré par la balise `h1`. L'ensemble, le titre + les paragraphes autour d'un sujet seront encadré par une balise `article`.


![](https://wptemplates.pehaa.com/assets/alyra/text-pandaroux.png)

![](https://wptemplates.pehaa.com/assets/alyra/html-pandaroux.png)

https://codepen.io/alyra/pen/bGeywNy

## Métaphore

![rangement ikea](https://s3-us-west-2.amazonaws.com/s.cdpn.io/4515922/wardrobe.jpg)

J'aime comparer la structure HTML d'un document web à un rangement Ikea. Les balises sont des placards, des étagères, des tiroirs, des boîtes, des cintres... 
- Chaque élément à son usage spécifique (comme une balise a son sens sémantique). Nous n'accrochons pas des chaussettes sur les cintres et nous ne mettons pas des costumes dans les tiroirs.
- Les éléments sont emboîtés l'un dans l'autre - mais pas tout à fait librement - par exemple, nous ne mettons pas de cintres dans les tiroirs. Pareil, dans HTML nous n'encadrons pas un titre par un paragraphe.
- Les éléments du même type peuvent avoir leurs spécificité (par exemple un tiroir magnétique). Nous pouvons aussi leur donner des étiquettes (accrocher un autocollant chaussettes 🧦 sur un tiroir, marqués certains placards "hiver", etc.)

## Anatomie d'un élément HTML

```html
<nomdebalise>contenu de l'élément</nomdebalise>
```

![](https://wptemplates.pehaa.com/assets/alyra/balises-html1.png)

Éléments HTML peuvent aussi avoir des attributs (caractéristiques et étiquettes).  
L'ordre dans lequel nous listons des attributs n'a pas d'importance. Les valeurs devrait être encadrées par des guillemets (`""`).

```html
<nomdebalise attribut1="sa valeur" attribut2="sa valeur">contenu de l'élément</nomdebalise>
```

![](https://wptemplates.pehaa.com/assets/alyra/balises-html2.png)

Il existe aussi des éléments qui n'ont pas de contenu, des éléments vides. Dans ce cas-là, nous allons utiliser des balises *auto-fermantes* (en anglais *self-closing tags*).  
Les exemples les plus simples des éléments vides sont :
- `<br />` - saut à la ligne (`<br>` est aussi correcte),
- `<hr />` - la ligne horizontale (`<hr>` est aussi correcte),

L'élément vide le plus souvent utilisé est `img`. La balise `img` permet d'afficher des images 🌄. L'élément `<img>` a toujours deux attributs 
- `src` - la source d'image à afficher
- `alt` - le texte qui décrit le contenu de l'image (texte alternatif).

```html
<img src="path/to/myimage.png" alt="Le contenu de mon image" />
```

ou 

```html
<img src="path/to/myimage.png" alt="Le contenu de mon image">
```

https://codepen.io/alyra/pen/zYBQoWe

## Structure du document HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Métadonnées du document -->
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

Revenons à notre métaphore "rangement Ikea". Le `body` du document html correspond au rangement lui-même. Mais seront nous capable de l'assembler sans sa notice (partie `head` du document html) ?

L'élément HTML `<head>` fournit des informations générales (métadonnées) sur le document. Les plus important sont :
- le titre du document
- liens ou des définitions vers des scripts et feuilles de style
- le jeux de caractères utilisé



<a href="https://s3-us-west-2.amazonaws.com/s.cdpn.io/4515922/removehead.mp4" target="_blank" rel="noreferrer noopener">Voici ce qui se passe quand on enlève la partie head.</a>

## Classement des balises HTML

Ci-dessous vous trouverez les principales balises HTML **classées par le contexte d'utilisation.**

Attention: Cette liste n'est pas 100% complète. Dans un objectif de clarté, certaines balises rarement utilisées, obsoletes ou "expérimentales" ne sont pas inclues. Vous pouvez en lire davantage dans la ["Référence des éléments HTML"](https://developer.mozilla.org/fr/docs/Web/HTML/Element)

### Racine principale (root)

`html`

### Métadonnées du document

`head`  
`base`  
`link`  
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
<noscript>Pour recevoir nos salutations, veillez activer JavaScript dans votre navigateur :)</noscript>
```

Vous pouvez voir le code ci-dessus en action en cliquant [ce lien](https://cdpn.io/alyra/debug/1a70873c7b9713e08a6d00b45ee1b0ab) et ensuite en désactivant JavaScript dans votre navigateur et en rechargeant la page.

### Tables

**Objectif** : Mettre le contenu dans les cases 😉

`table`  
`thead` `tbody` `tfoot`  
`tr` `td` `th`  
`colgroup` `col`

### Formulaires

**Objectif** : Envoyer des données !!!

`form`  
`fieldset`  
`legend`  
`label`  
`button`  
`input`  
`select`  
`optgroup`  
`option`  
`progress`  
`textarea`

### Éléments interactifs

`details` + `summary`

### Éléments obsoletes ⚠️

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

Chaque élément HTML est membre d'un certain nombre de catégories de contenu (par exemple _phrasing content_ ou _interactive content_). Il existe plusieurs règles qui sont basés sur ce classement. En particulier, certain éléments peuvent contenir uniquement des éléments appartenant à la classe *contenu phrasé*. 

### Phrasing content (contenu phrasé)

`a` (s'il contient lui-même _phrasing content_)  
 `abbr` `audio` `b` `bdo` `br` `button` `canvas` `cite` `code` `command` `data` `datalist` `dfn` `em` `embed` `i` `iframe` `img` `input` `kbd` `keygen` `label` `mark` `math` `meter` `noscript` `object` `output` `picture` `progress` `q` `ruby` `samp` `script` `select` `small` `span` `strong` `sub` `sup` `svg` `textarea` `time` `var` `video` `wbr` et texte.

Une des balise que nous utilisons particulierement souvent est `p` (paragraphe). Il est important de savoir que pour un paragraphe le seul contenu autorisé est contenu phrasé.

```html
<!-- ceci est correct (et vrai) -->
<p>Ca se complique, hein ? Ne vous inquiétez pas, on va continuer doucement en veillant que vous appreniez de bonnes pratiques.</p>

<!-- ceci n'est pas correct (et faux) -->
<p><div>Pfff, c'est trop compliqué.</div></p>
```

Regardons ensemble, le code dans le pen suivant. Pourquoi le texte n'est pas écrit en rouge tomate ??? 🤔

https://codepen.io/alyra/pen/QWjJzRB

**Comment savoir ?**

- Suivre la spécifation - [MDN - Référence des éléments HTML](https://developer.mozilla.org/fr/docs/Web/HTML/Element)
- [Veiller à toujours valider son document HTML](https://validator.w3.org/)

### Ressources

- [MDN - Référence des éléments HTML](https://developer.mozilla.org/fr/docs/Web/HTML/Element)
- [HTML Reference](https://htmlreference.io/)

---

## Exercices (2 jours)

- [Lecture obligatoire (MDN)](https://developer.mozilla.org/fr/docs/Apprendre/Commencer_avec_le_web/Les_bases_HTML)
- [Sac de voyage](https://codepen.io/alyra/pen/yLYxEpJ) | [solution](https://codepen.io/alyra/pen/50e0ae1bd5d18d37e3f239c6d673c1d1)
- [Trottinette](https://codepen.io/alyra/pen/vYNzrav) | [solution](https://codepen.io/alyra/pen/03cdc8f33f5523d04ba8ac8c9c5a615b)
- [Personnages Star Wars](https://codepen.io/alyra/pen/QWjPjMz) | [solution](https://codepen.io/alyra/pen/aab636e7598ee96a853e589048316ed0)
- [Portfolio de Sonia](https://codepen.io/alyra/pen/PoPXqVy) | [solution](https://codepen.io/alyra/pen/c0ef3d8ffd9ed715e85f8a3665694057)
- [Jamais sans passer par Markup Validation W3c](https://codepen.io/alyra/pen/JjYaZZL) | [solution](https://codepen.io/alyra/pen/0c8fdb50e2715f0dc4bd3e7ae555f220)
- [Divitis](https://codepen.io/alyra/pen/yLYxEvJ) | [solution](https://codepen.io/alyra/pen/09a63aef27a9616d22ea61ddaf214010)
- [Personal Landing Page](https://codepen.io/alyra/pen/WNQgyBw) | [solution](https://codepen.io/alyra/pen/b950fa9db46fd30932aadb41562dd400)
