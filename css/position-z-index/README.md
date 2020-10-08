# Position & z-index

![Mask](https://assets.codepen.io/4515922/mask.jpg)

Propriété `position` (encore une propriété au pouvoir magique) :

- static (par défaut, magie n'opère pas)
- relative
- absolute
- fixed
- sticky

### `position: static;`

❌ élément sort du layout (retiré du flux normal)  
❌ top, bottom, left, right activés  
❌ élément crée stacking-context  
❌ élément positionné = crée des coordonnées pour ses enfants

### `position: relative;`

❌ élément sort du layout (retiré du flux normal)  
✅ top, bottom, left, right (décalage d'élément par rapport à sa position initialle)  
✅ élément crée stacking-context  
✅ élément positionné = élément crée des coordonnées pour ses enfants

### `position: absolute;`

✅ élément sort du layout (retiré du flux normal)  
✅ top, bottom, left, right (position par rapport à l'ancêtre le plus proche qui est positionné ou html)  
✅ élément crée stacking-context  
✅ élément positionné = élément crée des coordonnées pour ses enfants

### `position: fixed;`

✅ élément sort du layout (retiré du flux normal)  
✅ top, bottom, left, right (position par rapport au bords de l'écran)  
✅ élément crée stacking-context  
✅ élément positionné = élément crée des coordonnées pour ses enfants

### `position: sticky;`

❌ élément sort du layout (retiré du flux normal)  
✅ top, bottom, left, right (position par rapport à l'ancêtre le plus proche qui est positionné ou html)  
✅ élément crée stacking-context  
✅ élément positionné = élément crée des coordonnées pour ses enfants

![Pochettes - métaphore de stacking-context](https://assets.codepen.io/4515922/pochettes.jpg)

[Essayons ensemble](https://codepen.io/alyra/pen/abdBvEQ)

[Exemple - masque](https://codepen.io/alyra/pen/XWXjOvV)
