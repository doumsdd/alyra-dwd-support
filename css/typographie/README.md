# Typographie

Vous l'avez peut-être déjà remarqué, certaines propriétés CSS se transmettent du parent vers enfant, d'autres non.

Les propriétés relatives au texte se héritent.

Par exemple, si vous fixez une color et une font-family pour body, tout élément sera mis en forme avec cette même couleur et cette même police, **à moins qu'on lui ait appliqué directement des règles.**

### font-family

```css
body {
  font-family: Helvetica, Arial, sans-serif;
}
```

#### Generic font-faces :

- serif
- sans-serif
- cursive
- fantasy
- monospace

[[[pen slug-hash='eYJOaOO' height='300' theme-id='1']]]

[Web-safe Fonts](https://www.cssfontstack.com/)

### font-weight

100 - 200 - 300 - ... - 900  
normal (400) - défaut pour body  
bold (700)

```
header p {
  font-weight: bold;
}
```

#### font-style

italic, normal

```
header p {
  font-style: italic;
}
```

#### font-size

`px`, `em`, `rem`

[[[pen slug-hash='VweZJzR' height='300' theme-id='1']]]

#### autres propriétés :

`text-decoration`  
`text-align` - alignement au sein d'un élément block  
`line-height`

- [Wanted Dead or Alive - Google Fonts](https://codesandbox.io/s/police-rxtme?file=/index.html) | [solution](https://codepen.io/alyra/pen/6eba070d53ff9fa1f9b0952d6ace935f)
