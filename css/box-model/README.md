# Box Model 📦

Propriétés qui définissent combien de place prend un élément :

`width` `height` `padding` `border` `margin`

### inline & block

`p, div, h1-h6, section, ...`, en fait la majorité des éléments est type `block`  
`span, em, strong, i, b, ins, del ...` - ont le caractère en-ligne `inline`

Le comportement d'un élément peut être modifier avec la propriété `display`

https://codepen.io/alyra/pen/YzwKodK

### margin & padding syntax

```css
div {
  padding: 20px;
  /*
  padding-top: 20px;
  padding-right: 20px;
  padding-bottom: 20px;
  padding-left: 20px;
  */
}
```

```css
div {
  padding: 20px 30px;
  /*
  padding-top: 20px;
  padding-right: 30px;
  padding-bottom: 20px;
  padding-left: 30px;
  */
}
```

```css
div {
  padding: 20px 30px 40px;
  /*
  padding-top: 20px;
  padding-right: 30px;
  padding-bottom: 40px;
  padding-left: 30px;
  */
}
```

```css
div {
  padding: 20px 30px 40px 50px;
  /*
  padding-top: 20px;
  padding-right: 30px;
  padding-bottom: 40px;
  padding-left: 50px;
  */
}
```

https://codepen.io/alyra/pen/XWXWRXJ

### Collapsing margins (marges fusionnées)

Les marges top et bottom des blocs sont parfois fusionnées en une seule marge.  
La taille de la marge = la plus grande des deux marges fusionnées. C'est ce qu'on appelle _collapsing margins._

Ceci concerne les situations suivantes:

- des éléments voisins adjacents
- aucun contenu séparant le parent et ses descendants
- bloc vides

https://codepen.io/alyra/pen/QWyWprr

### box-sizing

```css
* {
  box-sizing: border-box;
}
```

```css
html {
  box-sizing: border-box;
}
*,
*:before,
*:after {
  box-sizing: inherit;
}
```

[Playground](https://cdpn.io/alyra/debug/416abba364963b2efce1b467ed776f87)
