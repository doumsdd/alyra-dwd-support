# Tables

## Structure et HTML tags

`table`  
`thead` `tbody` `tfoot` - imbrique ensemble de lignes selon leurs fonction  
`tr` - ligne de cellules dans un tableau  
`th` `td` - cellules (en-tête et donnée)

`caption` - optionnel

```html
<table>
  <caption>
    Optionnel - description
  </caption>
  <!-- thead est optionnel, imbrique des lignes d'en-tête des colonnes d'un tableau. -->
  <thead>
    <tr>
      <th>titre 1</th>
      <th>titre 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>el 1</td>
      <td>el 2</td>
    </tr>
    <tr>
      <td colspan="2">el 3</td>
    </tr>
  </tbody>
  <!-- tfoot est optionnel, imbrique des lignes qui résument les colonnes d'un tableau. -->
  <tfoot>
    <tr>
      <td>el 4</td>
      <td>el 5</td>
    </tr>
  </tfoot>
</table>
```

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="html,result" data-user="alyra" data-slug-hash="PoPvKEV" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Qu'est qui va pas ici ? ">
  <span>See the Pen <a href="https://codepen.io/alyra/pen/PoPvKEV">
  Table - exemple </a> by Alyra (<a href="https://codepen.io/alyra">@alyra</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<!---
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
-->

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="result" data-user="alyra" data-slug-hash="dyYQLPE" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Live Coding - HTML table - Mes repas de la semaine">
  <span>See the Pen <a href="https://codepen.io/alyra/pen/dyYQLPE">
  Live Coding - HTML table - Mes repas de la semaine</a> by Alyra (<a href="https://codepen.io/alyra">@alyra</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<!---
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
-->


---

## Exercices

 - [Table de multiplication](https://codepen.io/alyra/pen/VwvVoRa) | [solution](https://codepen.io/alyra/pen/0c64510eac62c096c3cb3140d448deb2)
 - [Table (Candidat -> Certification)](https://codepen.io/alyra/pen/yLYQrjq) | [solution](https://codepen.io/alyra/pen/73226cb6ba6d469a91a721036a04faea)
 - [Tables - ALYRA (Challenge)](https://codepen.io/alyra/pen/LYpMPOx) | [solution](https://codepen.io/alyra/pen/cacca459f15f134825dcc8e51d87f674)