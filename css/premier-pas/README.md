## Syntaxe

```css
/*
selecteur  {
  propriété1: sa valeur;
  propriété2: sa valeur;
}
*/
p {
  color: red;
  letter-spacing: 2px;
}
```

## Comment lier CSS à un doc HTML

Pour que les styles soient bien appliqués aux éléments dans le document HTML, leurs déclaration doivent être visible dans ce document.

Ceci peut être effectué à plusieurs façons :

1. Les déclarations css sont écrits dans un fichier séparé. Ce fichier aura pour extention `.css`, par exemple `style.css`

Afin que le document HTML puisse "lire" les styles, nous devons ajouter une balise dans la partie `head` du document, comme ci-dessous :

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- .. -->
    <link rel="stylesheet" href="chemin/vers/le/fichier/style.css" />
    <!-- .. -->
  </head>
</html>
```

2. Les déclarations de styles peuvent être aussi inclues directement dans le `head` (sans passer par un fichier séparé). Dans ce cas là, on utilise les balises `<style>`

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- .. -->
    <style>
      p {
        color: red;
        letter-spacing: 2px;
      }
      h1 {
        color: magenta;
      }
    </style>
    <!-- .. -->
  </head>
</html>
```

3. On peut aussi appliquer des styles css à un élément directement dans HTML, avec un attribut `style`

```html
<p style="color: crimson; letter-spacing: 3px;">
  Haha ! Je crois que je vais rougir !
</p>
```

## Exercices

 - [Texte](https://codepen.io/alyra/pen/XWmGaxE) | [solution](https://codepen.io/alyra/pen/71324a74c0b4cc0eeafc258ca92ecff9)
 - [Ajouter des classes](https://codepen.io/alyra/pen/VwvRzRJ) | [solution](https://codepen.io/alyra/pen/9bba5bbe25f5173c3356816078256b0e)
 - [Sac à dos](https://codepen.io/alyra/pen/LYpwabq) | [solution](https://codepen.io/alyra/pen/adce46c948e55c0792b03f7deee72700)
 - [Trottinette ](https://codepen.io/alyra/pen/abvMLBM) | [solution](https://codepen.io/alyra/pen/10ebf7eee701d8cb292a9561a0d40c2a)
 - [Chotto Motto](https://codepen.io/alyra/pen/mdeoBqr) | [solution](https://codepen.io/alyra/pen/6d30ffdd107e2dadd630433d5cd5aa61)

