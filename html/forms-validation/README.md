# Validation de Formulaires

C'est le rôle de développeur front-end d'assurer que les données soumises par un utilisateur via un formulaire sont dans un format correct. Nous parlons ici de la validation côté-client (_client-side validation_). La validation _client-side_ s'ajoute à la validation côté serveur (_server-side validation_). Elle n'est pas pourtant moins importante et ne devrait pas être négligé. De cette façon nous aidons les utilisateur en leur donnant un feedback instantané sur leurs saisies. C'est absolument nécessaire pour dans le contexte de bonne expérience utilisateur.

Avec l'arrivée de _HTML5_ nous avons la validation "nativement" disponible dans le navigateur. Nous pouvons spécifier le format souhaiter grace aux attribut html. L'élément `form` bloquera l'envoie des données si les formats ne sont pas respectés.

Nous avons à notre disposition :

- l'attribut `type` pour les contrôle `input` qui impose le format (par exemple `<input type="email">` impose le format d'addresse mail correcte)
-


## Pattern

Symbole | Signification
--- | ---
`.` | Caractère générique : correspond à tout caractère à l'exception de la nouvelle ligne (\n)
`(a\|b)` | a ou b
`[abc]` | un de a, b, c
`[^abc]` | aucun de a - c
`[^abc]` | aucun de a - c
`[a-q]` | caractère dans la plage de a à q (minuscules)
`[A-Q]` | caractère dans la plage de   A à Q (majuscules)
`[0-7]` | Chiffre entre 0 et 7
`\d` | chiffre décimal
`\D` | caractère autre qu’un chiffre décimal
`\s` | tout caractère espace blanc</div>
`\S` | tout caractère autre qu’un espace blanc
`*` | 0 ou plus
`{3}` | Exactement 3
`+` | 1 ou plus
`{3,}` | 3 ou plus
`?` |  0 ou 1
`{3,5}` |  3, 4 ou 5
