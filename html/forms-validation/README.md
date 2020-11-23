# Validation de Formulaires

C'est le rôle de développeur front-end d'assurer que les données soumises par un utilisateur via un formulaire sont dans un format correct. Nous parlons ici de la validation côté-client (_client-side validation_). La validation _client-side_ s'ajoute à la validation côté serveur (_server-side validation_). Elle n'est pas pourtant moins importante et ne devrait pas être négligée. Un des avantages est le feedback instantané envoyé à l'utilisateur sur ses saisies. C'est absolument nécessaire pour dans le contexte de bonne expérience utilisateur.

Avec l'arrivée de _HTML5_ nous avons la validation _"nativement"_ disponible dans le navigateur. Nous pouvons spécifier le format souhaité grâce aux attributs HTML. L'élément `form` bloquera l'envoie des données si les formats ne sont pas respectés.

Nous avons à notre disposition :

- l'attribut `type` pour les contrôles `input` qui impose le format (par exemple `<input type="email">` impose le format d'addresse mail correcte)

```html
<label for="mail">Votre adresse e-mail</label>
<input id="mail" name="mail" type="email" placeholder="ex. mr@alyra.fr">
```

- l'attribut `required` qui indique que le champs doit être rempli

```html
<label for="mail">Votre adresse e-mail</label>
<input id="mail" name="mail" type="email" placeholder="ex. mr@alyra.fr" required>
```

## Pattern

<table><tbody><tr><td><code>.</code></td><td>Caractère générique : correspond à tout caractère à l'exception de la nouvelle ligne (\n)</td></tr><tr><td><code>(a|b)</code></td><td>a ou b</td></tr><tr><td><code>[abc]</code></td><td>Un de (a ou b ou c)</td></tr><tr><td><code>[^abc]</code></td><td>Aucun de (a ou b ou c)</td></tr><tr><td><code>[a-q]</code></td><td>caractère dans la plage de a à q (minuscules)</td></tr><tr><td><code>[A-Q]</code></td><td>caractère dans la plage de A à Q (majuscules)</td></tr><tr><td><code>[0-7]</code></td><td>Chiffre entre 0 et 7</td></tr><tr><td><code>\d</code></td><td >chiffre décimal</td></tr><tr><td><code>\D</code></td><td>aractère autre qu’un chiffre décimal</td></tr><tr><td><code>\s</code></td><td>tout caractère espace blanc</td></tr><tr><td><code>\S</code></td><td>tout caractère autre qu’un espace blanc</td></tr></tbody></table>

<table><tbody><tr><td><code>*</code></td><td>0 ou plus</td></tr><tr><td><code>{3}</code></td><td>Exactement 3</td></tr><tr><td><code>+</code></td><td>1 ou plus</td></tr><tr><td><code>{3,}</code></td><td>3 ou plus</td></tr><tr><td><code>?</code></td><td>0 ou 1</td></tr><tr><td><code>{3,5}</code></td><td>3, 4 ou 5</td></tr></tbody></table>
