# Validation de Formulaires

C'est le rôle de développeur front-end d'assurer que les données soumises par un utilisateur via un formulaire sont dans un format correct. Nous parlons ici de la validation côté-client (_client-side validation_). La validation _client-side_ s'ajoute à la validation côté serveur (_server-side validation_). Elle n'est pas pourtant moins importante et ne devrait pas être négligé. De cette façon nous aidons les utilisateur en leur donnant un feedback instantané sur leurs saisies. C'est absolument nécessaire pour dans le contexte de bonne expérience utilisateur.

Avec l'arrivée de _HTML5_ nous avons la validation "nativement" disponible dans le navigateur. Nous pouvons spécifier le format souhaiter grace aux attribut html. L'élément `form` bloquera l'envoie des données si les formats ne sont pas respectés.

Nous avons à notre disposition :

- l'attribut `type` pour les contrôle `input` qui impose le format (par exemple `<input type="email">` impose le format d'addresse mail correcte)
-