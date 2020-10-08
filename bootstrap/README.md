# Bootstrap 5

Bootstrap est une librairie open-source qui unifie et accélère la mise en page. Comme avec n'importe quelle bibliothèque, il est indisponsable d'apprendre se servir de sa documentation. Vous trouverez la documentation de bootstrap sur [le site officiel de Bootstrap 5](https://v5.getbootstrap.com/)

## Comment s'en servir ?

Bootstrap vient avec un grand fichier <code>.css</code> déja écrit.
Ceci dit, la grande partie de la mise en page se passera dans les
fichiers <code>.html</code> où nous appliquerons des classes définies
dans le stylesheet de bootstrap.

Il faut un peu de temps et de la pratique pour apprivoiser cette
approche. Mais, attention, c'est un bon investissement, puisque c'est
une approche qui <b>accélère</b> le processus de déveleppement.

Nous devons alors en même temps apprendre à se servir de [la documentation](https://v5.getbootstrap.com/docs/5.0/getting-started/introduction/)
et comprendre la logique des noms des classes.

## Que fait le fichier css de bootstrap ?

- met en place une solution basée sur normalize.css
- met `* {box-sizing: border-box;}`
- expose une grande nombre des classes css, prêtes à utiliser

- couleurs
- typographie
- espacements
- layout
- formulaires
- barre de navigation (responsive avec JavaScript)
- met en place des composents (modals, alerts
- et ce n'est pas tout

Si vous vous rappelez de [cet exercice](https://codepen.io/alyra/details/VwvRzRJ), c'est le même concepte, sauf que le nombre des classes css est beaucoup plus important...

Et si cela vous intéresse, voici [le coupable](https://codepen.io/alyra/pen/eeebfe01507653f20f9193f3ae5cf1ea.css) - attention, il contient presque 10k lignes 🤯.

## Mise en place

**Starter template**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />

    <!-- Bootstrap CSS -->
    <link
      rel="stylesheet"
      href="https://stackpath.bootstrapcdn.com/bootstrap/5.0.0-alpha1/css/bootstrap.min.css"
      integrity="sha384-r4NyP46KrjDleawBgD5tp8Y7UzmLA05oM1iAEQ17CSuDqnUK2+k9luXQOfXJCJ4I"
      crossorigin="anonymous"
    />

    <title>Hello, world!</title>
  </head>

  <body>
    <h1>Hello, world!</h1>
    <!-- ... -->
    <!-- Optional JavaScript -->
    <!-- Popper.js first, then Bootstrap JS -->
    <script
      src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"
      integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo"
      crossorigin="anonymous"
    ></script>
    <script
      src="https://stackpath.bootstrapcdn.com/bootstrap/5.0.0-alpha1/js/bootstrap.min.js"
      integrity="sha384-oesi62hOLfzrys4LxRF63OJCXdXDipiYWBnvTl9Y9/TRlw5xlKIEHpNyvvDShgf/"
      crossorigin="anonymous"
    ></script>
  </body>
</html>
```

### Couleurs

Nous pouvons appliquer des classes <code>.bg-..</code> et
<code>.text-..</code> afin d'appliquer des couleurs prédefinies par
bootstrap.

[Docs > Utilities > Colors](https://v5.getbootstrap.com/docs/5.0/utilities/colors/)

## Espacements

### Breakpoints

<table class="table" style="width: 100%">
  <thead>
    <tr>
      <th>Breakpoint</th>
      <th>Class infix</th>
      <th>Dimensions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>X-Small</td>
      <td><em>None</em></td>
      <td>0–576px</td>
    </tr>
    <tr>
      <td>Small</td>
      <td><code>sm</code></td>
      <td>≥576px</td>
    </tr>
    <tr>
      <td>Medium</td>
      <td><code>md</code></td>
      <td>≥768px</td>
    </tr>
    <tr>
      <td>Large</td>
      <td><code>lg</code></td>
      <td>≥992px</td>
    </tr>
    <tr>
      <td>Extra large</td>
      <td><code>xl</code></td>
      <td>≥1200px</td>
    </tr>
    <tr>
      <td>Extra extra large</td>
      <td><code>xxl</code></td>
      <td>≥1400px</td>
    </tr>
  </tbody>
</table>

Nous pouvons appliquer des classes <code>p..-..</code> et
<code>m..-..</code> afin d'appliquer des paddings et des margins prédefinis par bootstrap.

```html
<p class="m-0">Je suis un paragraphe et je mets mes marges à zéro</p>
```

```html
<section class="p-4">
  Je suis une section et je mets des paddings de 1.5rem.
</section>
```

```html
<section class="p-md-5">
  Je suis une section et je quand l'écran dépasse 768px je mets des paddings de
  3rem.
</section>
```

```html
<section class="p-3 p-md-5">
  Je suis une section je mets des paddings de 1rem mais quand l'écran dépasse
  768px je les change pour de 3rem.
</section>
```

<a href="https://v5.getbootstrap.com/docs/5.0/utilities/spacing/"
              >Docs > Utilities > Spacing</a
            >

Syntaxe : `p{side}-{breakpoint}-{size}`

<dl>
  <dt><code>p-0</code></dt>
  <dd><code>.p-0 {padding: 0;}</code></dd>
  <dt><code>p-1</code></dt>
  <dd><code>.p-1 {padding: .25rem;}</code></dd>
  <dt><code>p-2</code></dt>
  <dd><code>.p-2 {padding: .5rem;}</code></dd>
  <dt><code>p-3</code></dt>
  <dd><code>.p-3 {padding: 1rem;}</code></dd>
  <dt><code>p-4</code></dt>
  <dd><code>.p-4 {padding: 1.5rem;}</code></dd>
  <dt><code>p-5</code></dt>
  <dd><code>.p-5 {padding: 3rem;}</code></dd>
</dl>
<dl>
  <dt><code>pt-0</code></dt>
  <dd><code>.pt-0 {padding-top: 0;}</code></dd>
  <dt><code>pr-1</code></dt>
  <dd><code>.pr-1 {padding-right: .25rem;}</code></dd>
  <dt><code>pb-2</code></dt>
  <dd><code>.pb-2 {padding-bottom: .5rem;}</code></dd>
  <dt><code>pl-3</code></dt>
  <dd><code>.pl-3 {padding-left: 1rem;}</code></dd>
  <dt><code>px-4</code></dt>
  <dd>
    <code>.px-4 {padding-left: 1.5rem; padding-right: 1.5rem;}</code>
  </dd>
  <dt><code>py-5</code></dt>
  <dd>
    <code>.py-5 {padding-top: 3rem; padding-bottom: 3rem;}</code>
  </dd>
</dl>
<p>
  Le même système s'applique aux margins, avec quelques classes en
  plus <code>m{sides}-auto</code>
</p>
<dl>
  <dt><code>m-auto</code></dt>
  <dd><code>.m-auto {margin: auto;}</code></dd>
  <dt><code>mt-auto</code></dt>
  <dd><code>.mt-auto {margin-top: auto;}</code></dd>
  <dt><code>mr-auto</code></dt>
  <dd><code>.mr-auto {margin-right: auto;}</code></dd>
  <dt><code>ml-auto</code></dt>
  <dd><code>.ml-auto {margin-left: auto;}</code></dd>
  <dt><code>mx-auto</code></dt>
  <dd><code>.mx-auto {margin-left: auto; margin-right: auto;}</code></dd>
  <dt><code>my-auto</code></dt>
 <dd><code>.my-auto {margin-top: auto; margin-bottom: auto;}</code></dd>
</dl>

### Système de grid bootstrap

La grille de bootstrap est, comme la plupart des systèmes de grille, basée sur **12** colonnes.

![grid](https://assets.codepen.io/4515922/BlogArticle-BootstrapGrid.png)

Les noms de classes correspondent au nombre de colonnes occupées.

```html
<div class="container">
  <div class="row">
    <div class="col-6">Je prends la place de 6 colonnes sur 12</div>
    <div class="col-6">Je prends la place de 6 colonnes sur 12</div>
  </div>
</div>
```

[Exemple](https://codepen.io/alyra/pen/dyGWJjx)

### Navigation

- [navs dans la doc bootstrap](https://v5.getbootstrap.com/docs/5.0/components/navs/) & [navbars dans la doc bootstrap](https://v5.getbootstrap.com/docs/5.0/components/navbar/)
- [exemple CodePen](https://codepen.io/alyra/pen/YzwVeQG)

### Bootstrap Icons

[Documentation](https://icons.getbootstrap.com/)

### Bonjour Bootstrap Live

[Live coding start](https://codepen.io/alyra/pen/JjGNOKN) - [rendu final](https://cdpn.io/alyra/debug/7855e2a6ac75130ab07c8201ad3e5d44)

---

[Exemples officiels Bootstrap](https://v5.getbootstrap.com/docs/5.0/examples/)

## Exercices

- [B5 - text](https://codepen.io/alyra/pen/GRorKox) | [solution](https://codepen.io/alyra/pen/3f97ec03324f5cf55daa6f97618ea43e)
- [B5 - section](https://codepen.io/alyra/pen/rNxjNpJ) | [solution](https://codepen.io/alyra/pen/d6a277fe5a33b558335b0904c151803a)
- [B5 - m/p/colors](https://codepen.io/alyra/pen/RwrKZzg) | [solution](https://codepen.io/alyra/pen/137a55fd1a91de2232e60ff936b2807e)
- [B5 - responsive grid](https://codepen.io/alyra/pen/jOWLNOw) | [solution](https://codepen.io/alyra/pen/03d919fda707fa50b382679e2a5474db)
- [B5 - responsive grid (2)](https://codepen.io/alyra/pen/ExPZwWK) | [solution](https://codepen.io/alyra/pen/85688979ba506492bce387099c80bc93)
