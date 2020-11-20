# Validation de Formulaires

C'est le rôle de développeur front-end d'assurer que les données soumises par un utilisateur via un formulaire sont dans un format correct. Nous parlons ici de la validation côté-client (_client-side validation_). La validation _client-side_ s'ajoute à la validation côté serveur (_server-side validation_). Elle n'est pas pourtant moins importante et ne devrait pas être négligé. De cette façon nous aidons les utilisateur en leur donnant un feedback instantané sur leurs saisies. C'est absolument nécessaire pour dans le contexte de bonne expérience utilisateur.

Avec l'arrivée de _HTML5_ nous avons la validation "nativement" disponible dans le navigateur. Nous pouvons spécifier le format souhaiter grace aux attribut html. L'élément `form` bloquera l'envoie des données si les formats ne sont pas respectés.

Nous avons à notre disposition :

- l'attribut `type` pour les contrôle `input` qui impose le format (par exemple `<input type="email">` impose le format d'addresse mail correcte)
-


## Pattern

<table border="0" cellspacing="0" cellpadding="0">
  <tbody>
    <tr>
      <td valign="top">
        <div style="padding: 3px 8px;">.</div></td>
      <td valign="top">
        <div style="padding: 3px 8px;">Caractère générique : correspond à tout caractère à l'exception de la nouvelle ligne (\n)</div>
      </td>
    </tr>
    <tr>
      <td valign="top">
        <div style="padding: 3px 8px;">(a|b)</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">a ou b</div>
      </td>
    </tr>
    <tr>
      <td valign="top">
        <div style="padding: 3px 8px;">[abc]</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">Un de (a ou b ou c)</div>         </td>
    </tr>
    <tr class="countrow">
      <td valign="top">
        <div style="padding: 3px 8px;">[^abc]</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">Aucun de (a ou b ou c)</div>            </td>
    </tr>
    <tr class="altrow countrow">
      <td valign="top">
        <div style="padding: 3px 8px;">[a-q]</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">caractère dans la plage de a à q (minuscules)</div>
      </td>
    </tr>
    <tr>
      <td valign="top">
        <div style="padding: 3px 8px;">[A-Q]</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">caractère dans la plage de   A à Q (majuscules)</div>
      </td>
    </tr>
    <tr>
      <td valign="top">
        <div style="padding: 3px 8px;">[0-7]</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">Chiffre entre 0 et 7</div>
      </td>
    </tr>
    <tr class="countrow"><td valign="top">
      <div style="padding: 3px 8px;">\d</div>
      </td>
      <td valign="top" class="cheat_sheet_output_cell_2">
        <div style="padding: 3px 8px;">chiffre décimal</div>
      </td>
    </tr>
    <tr class="countrow"><td valign="top">
      <div style="padding: 3px 8px;">\D</div>
      </td>
      <td valign="top" class="cheat_sheet_output_cell_2">
        <div style="padding: 3px 8px;">caractère autre qu’un chiffre décimal</div>
      </td>
    </tr>
    <tr class="countrow"><td valign="top">
      <div style="padding: 3px 8px;">\s</div>
      </td>
      <td valign="top" class="cheat_sheet_output_cell_2">
        <div style="padding: 3px 8px;">tout caractère espace blanc</div>
      </td>
    </tr>
    <tr class="countrow"><td valign="top">
      <div style="padding: 3px 8px;">\S</div>
      </td>
      <td valign="top" class="cheat_sheet_output_cell_2">
        <div style="padding: 3px 8px;">tout caractère autre qu’un espace blanc</div>
      </td>
    </tr>
  </tbody>
</table>


<table border="0" cellspacing="0" cellpadding="0" >
  <tbody><tr class="altrow countrow">
    <td valign="top" >
      <div style="padding: 3px 8px;">*</div>
    </td>
    <td valign="top">
      <div style="padding: 3px 8px;">0 ou plus</div>
    </td>
    <td valign="top">
      <div style="padding: 3px 8px;">{3}</div>
    </td>
    <td valign="top">
      <div style="padding: 3px 8px;">Exactement 3</div>
    </td>
    </tr>
    <tr>
      <td valign="top">
        <div style="padding: 3px 8px;">+</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">1 ou plus</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">{3,}</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">3 ou plus</div>
      </td>
    </tr>
    <tr>
      <td valign="top">
        <div style="padding: 3px 8px;">?</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">0 ou 1</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">{3,5}</div>
      </td>
      <td valign="top">
        <div style="padding: 3px 8px;">3, 4 ou 5</div>
      </td>
    </tr>
  </tbody>
</table>
