# Strings - que pouvons nous faire avec ?

```javasscript
let message = "Parlons du type string !"
```

Vous vous rappelez bien que `"string"` est un des type prymitif dans JavaScript. Il existe plusieures méthodes que nous pouvons appliquer aux "strings" pour changer leur format ou récuperer des information spécifiques.


## 1. Quelle est la longueur d'un string ?

```javascript
message.length
```

Pourquoi est-ce important ? Par exemple, pour vérifier si la longeur du mot de pass est suffisante ?

**Exemple:**

```javascript
let answer = prompt("Ton password?")

if (answer.length < 8) {
  alert("Ton password semble trop court !")
}
```

## 2. Et si voulais le mettre en majuscule ?

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

## 3. On a besoin d'enlever les espaces au début et à la fin

```javascript
message = "  uhm...  "
message.trim()
// "uhm..."
```

## 4. Trouver la position d'un substring

Pour cela on utilise la méthode `.indexOf()` qui retourne la position (attention, on compte à partir de 0) ou `-1` si le substring n'est pas trouvé.

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

<div class="post-note">
On peut utiliser indexOf pour vérifier si le substring est présent, comme dans l'exemple ci-dessous.
</div>

**Exemple:**

```javascript
let answer = prompt("Listez vos écoles?")
if (answer.indexOf("Alyra") === -1) {
  alert("Vous n'avez pas mentionné Alyra")
}
```

## 5. Trouver le carectère selon la position

```javascript
message[0]
// ou
message.charAt(0)
message.charAt(10)
```

et sur la dernière position ?

Prenons 'Alyra' comme exemple, ce string a la valeur `'Alyra'.length` égale à 5, par contre les caractères sont comptés à partir de 0 alors le dernier a le numéro 4, ceci dit `'Alyra'.length - 1`

```javascript
message[message.length - 1]
// ou
message.charAt(message.length - 1)
```

## 6. Découper une partie du string

```javascript
let message = "Bonjour Alyra"
message.slice(0, 5) // 'Bonjo', de 0 à 5 (5 pas inclu)
message.slice(0, 1) // 'B', de 0 à 1, (1 pas inclu)
message.slice(8) // 'Alyra', de 8 à la fin
message.slice(8, 10) // 'Al', de 8 à 10, (10 pas inclu)
```

Voici comment on peut utiliser `slice` pour mettre en majuscule uniquement le premier caractère :

```javascript
let message = "bonjour"
message = message[0].toUpperCase() + message.slice(1)
// Bonjour
```

## 7. Depuis peu il existe aussi 3 méthodes `includes`, `startsWith` et `endsWith` 🤩

```javascript
let message = "Bonjour Alyra !"
message.includes("Alyra")
// true
message.startsWith("Bon")
// true
message.endsWith("!!")
// false
```

## Exercices

[JavaScript Quizzez - Strings](https://javascript-quizzes.netlify.app/strings)
