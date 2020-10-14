# Array - Introduction

PeHaa et son mari Vains ont pour habitude de faire leurs courses alimentaires le samedi matin, après leur petit déjeuner.
Ce samedi matin, en sirotant son café, PeHaa commence à noter tout ce qu'ils doivent acheter. Quoi de plus pratique qu'une liste 🗒:

```javascript
const listeCoursesPeHaa = ['tortillas', 'haricots', 'piment']
```

Comme vous pouvez vous en doûter, ce soir, burritos au menu 🌮! Et pas uniquement chez PeHaa et Vains. Inspirée par sa voisine et munie de la même recette super-easy, Anne-Françoise, note ce qui suit :

```javascript
const listeCoursesAF = ['tortillas', 'haricots', 'piment']
```

Première grande question : est-ce vrai que ```listeCoursesPeHaa === listeCoursesAF``` ?

Jusqu'à maintenant nous avons travaillé avec des valeurs de type "primitifs" (number, string, boolean, undefined). 
Les *arrays* ne sont pas de type primitifs, il sont de type 'object', voici la preuve :

```javascript
typeof(['tortillas', 'haricots', 'piment'])
// 'object'
```

Les valeurs primitives sont stockées et copiées en tant que telles. Ceci n'est pas vrai pour les objets. Quand un object est affecté à une variable, cette dernière ne stocke pas l'objet lui-même, mais son «adresse en mémoire», la «référence» de cet objet.

PeHaa et Anne-Françoise ont créé leurs listes independemment. La liste de PeHaa n'a pas la même adresse en mémoire que la liste d'Anne-Françoise. Ce sont 2 listes différentes. Même si elles sont tout à fait identiques.

```javascript
listeCoursesPeHaa === listeCoursesAF
// false
```

![](https://assets.codepen.io/4515922/difrefarray.png)

Revenons sur la liste de PeHaa. Elle se rapelle qu'elle vient d'utiliser le dernier oeuf en préparant des pancakes 🥞 ce matin. Alors, elle ajoute des oeufs à sa liste 

```javascript
listeCoursesPeHaa.push('oeufs')
console.log(listeCoursesPeHaa)
// ['tortillas', 'haricots', 'piment', 'oeufs']
```

La méthode `push` ajoute des nouveau éléments **à la fin** de l'array. Dans notre cas 'oeufs' est ajouté à la fin de l'array dont la référence est stockée dans `listeCoursesPeHaa`.

Attendez 🧐, la liste vient d'être modifiée. La variable a été déclarée avec le mot `const` - hey, console, comment ça, y a pas d'erreur ??!

Ben non, la liste était modifiée, mais son addresse en mémoire (sa référrence) est restée la même. Rappellons, que la variable `listeCoursesPeHaa` indique la référence, et non la liste.

"Hmmm, j'ai du oublier plein de choses, tu veux regarder, s'il te plaît :) ?" - demande PeHaa à son mari. 

Vains prend le relais : 

```javascript
const listeCoursesVains = listeCoursesPeHaa
listeCoursesVains.push('lasagnes', 'pizza', 'bières', 'clémentines')
```

"Je regarde ce que tu as ajouté" - dit PeHaa

```javascript
console.log(listeCoursesPeHaa)
// ['tortillas', 'haricots', 'piment', 'oeufs', 'lasagnes', 'pizza', 'bières', 'clémentines']
```

Attendez, quatre nouveaux ingrédients sur la liste de PeHaa. Qu'est ce qui vient de se passer ici ?

Analysons ça, étape par étape.  
Quand Vains a déclaré sa variable `listeCoursesVains`, il lui a affecté la valeur de `listeCoursesPeHaa`. Cette dernière est la référence de l'array que PeHaa a créé au début de cette histoire.
Maintenant `listeCoursesPeHaa` et `listeCoursesVains` indiquent toutes les deux l'adresse en mémoire de la même liste.

![](https://assets.codepen.io/4515922/samerefarray.png)

Les méthodes, comme :

- `push` (ajoute un élément à la fin de la liste) ,  
- `pop` (enlève le dernier élément)  
- `shift` (enlève le premier élément)  
- `unshift` (ajoute un élément au début de la liste)  
- `reverse`
- `splice`  
- `sort` (trie la liste)
peuvent être, avec le même effet, appliquée à la `listeCoursesPeHaa` ou à la `listeCoursesVains`. 
D'ailleurs...

"Tu sais, pour des clémentines, ce n'est pas tout à fait la saison... Je les enlève..."

```javascript
listeCoursesPeHaa.pop()
console.log(listeCoursesPeHaa)
// ['tortillas', 'haricots', 'piment', 'oeufs', 'lasagnes', 'pizza', 'bières']
console.log(listeCoursesVains)
// ['tortillas', 'haricots', 'piment', 'oeufs', 'lasagnes', 'pizza', 'bières']
```

Et ainsi ils sont partis, direction le supermarché 🛒.

PS. Si vous changez d'avis au dernier moment, que vous voulez écraser toute la liste et décidez : *diète, régime*

```javascript
listeCoursesPeHaa = []
// Uncaught TypeError: Assignment to constant variable.
```

Ceci n'est pas possible. Ici on vient de créer un nouvel objet (liste vide), un nouvel objet = une nouvelle adresse en mémoire (nouvelle référence). On essaye de réaffecter listeCoursesPeHaa qui était créée avec `const`. Ceci donne une erreur.


PS. Les personnages et les situations de ce récit étant purement fictifs, toute ressemblance avec des personnes ou des situations existantes ou ayant existé ne serait que pure coincidence.


