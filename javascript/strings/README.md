# Strings - que pouvons nous faire avec ?

```javascript
let message = "Parlons du type string !"
```

Vous vous rappelez bien que `"string"` est un des types primitifs dans JavaScript. Il existe plusieurs méthodes que nous pouvons appliquer aux "strings" pour changer leur format ou récupérer des informations spécifiques.


## 1. Quelle est la longueur d'un string ?

```javascript
message.length
```

Pourquoi est-ce important ? Par exemple, pour vérifier si la longueur du mot de pass est suffisante :

**Exemple:**

```javascript
let answer = prompt("Ton password?")

if (answer.length < 8) {
  alert("Ton password semble trop court !")
}
```

## 2. Et si on voulait mettre un string en majuscule, est-ce possible ?

```javascript
message.toUpperCase()
message.toLowerCase()
```

**Exemple:**

```javascript
let answer = prompt("Ton école?")

if (answer.toUppercase() === "ALYRA") {
  alert("Nous sont à la même école!")
}
```

On s'en sert souvent ? Oui ! Comme vous pouvez le voir ci-dessus, unifier la casse des lettres permet de faciliter la comparaison avec le string attendu.

## 3. Peut-on enlever les espaces au début et à la fin d'un string ?

Tout à fait. Nous utilisons la méthode `trim` et cela permet de "nettoyer" l'entrée d'utilisateur.

```javascript
message = "  uhm...  "
message.trim()
// "uhm..."
```

## 4. ... et trouver la position d'un substring ?

Pour cela on utilise la méthode `.indexOf()` qui retourne la position. Mais attention, avec JavaScript on compte à partir de 0. Si le substring n'est pas trouvé le résultat de `.indexOf()` est `-1`.

**Exemple:**

```javascript
let answer = "alyra"

answer.indexOf("a")
// 0, 'a' est à la première position alors 0 (on compte 0, 1, 2, ...)
answer.indexOf("y")
// 2, 'y' est à la 3e position alors 2 (on compte 0, 1, 2, ...)
answer.indexOf("r")
// 3, 'r' est à la 4e position alors 3 (on compte 0, 1, 2, ...)
answer.indexOf("b")
// -1, 'b' n'est pas trouvé !
```

Il existe aussi `lastIndexOf()`

```javascript
let answer = "alyra"
answer.lastIndexOf("a")
// 4, le dernier 'a' est à la 5e position, alors 4
```

Nous pouvons, par exemple, vérifier si un lien hypertexte commence par "#"

**Exemple:**

```javascript
let link1 = "#top"
// let link1 = "https://alyra.fr"
if (link1.indexOf("#") === 0) {
  console.log("link1 est un lien interne")
} else {
  console.log("link1 est un lien externe")
}
```

## 5. Trouver le caractère selon la position ?

Vous avez besoin de connaître le premier caractère d'un string? Ou le 10e. Rappelons-nous - avec JavaScript nous comptons à partir de zéro - les caractères sont numérotés à partir du zéro. Le premier caractère est celui avec l'index `0`. 

```javascript
message[0]
// ou
message.charAt(0)
message.charAt(10)
```

Et sur la dernière position ?

Prenons 'Alyra' comme exemple, ce string a la valeur `'Alyra'.length` égale à 5, par contre les caractères sont comptés à partir de 0 alors le dernier a le numéro 4, ceci dit `'Alyra'.length - 1`

```javascript
message[message.length - 1]
// ou
message.charAt(message.length - 1)
```

## 6. Découper une partie du string ?

```javascript
let message = "Bonjour Alyra"
message.slice(0, 5) // 'Bonjo', de 0 à 5 (5 pas inclus)
message.slice(0, 1) // 'B', de 0 à 1, (1 pas inclus)
message.slice(8) // 'Alyra', de 8 à la fin
message.slice(8, 10) // 'Al', de 8 à 10, (10 pas inclus)
```

Voici comment on peut utiliser `slice` pour mettre en majuscule uniquement le premier caractère :

```javascript
let message = "bonjour"
message = message[0].toUpperCase() + message.slice(1)
// Bonjour
```

## 7. Peut-on vérifier si le string contient, commence par ou finit par quelque chose ?

Oui on peut. Ceci est possible, avec des méthodes : `includes`, `startsWith` et `endsWith` 🤩

```javascript
let message = "Bonjour Alyra !"
message.includes("Alyra")
// true
message.startsWith("Bon")
// true
message.endsWith("!!")
// false
```

---

## Exercices

[JavaScript Quizzes - Strings](https://javascript-quizzes.netlify.app/strings)
