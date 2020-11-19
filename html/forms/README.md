# Formulaires

HTML fournit différents éléments afin de créer des formulaires. Formulaires permettent aux utilisateurs d'intéragir avec un site web ou une application. 

Les formulaires que nous utilisons le plus souvent sont :
- un champs de recherche au sein d'un site web 🔎
- formulaire de contact sur un site web 📩
- formulaire que nous remplissons afin d'effectuer un achat en-ligne 🛒

Nous allons apprendre comment mettre en place  des contrôles interactifs permettant à un utilisateur d'envoyer des données. (Ce qui se passe ensuite avec ces données, ne nous concerne pas pour l'instant.)

## <code>form</code>

Notre aventure commence avec l'élément `<form>`. `<form>` représente une section qui regroupe les élément interactifs.

```html
<form action="/ou/envoyer/" method="POST">
</form>
```

Je mentionne ici très brievement les attributs `action` et `method` :

- `action` - L'URL vers le script qui traitera les données envoyées par le formulaire. Nous serons redirigé vers cette adresse. Si `action` n'est pas spécifié, les données sont envoyées à l'URL de la page contenant le formulaire.
- `method` - comment les données sont envoyées, dans la majorité des cas les formulaires utilisent la méthode `GET` (méthode par défaut) ou `POST`. Avec la méthode GET les données sont envoyées via l'URL.  Avec la méthode POST les données sont envoyées dans le body de la requête.

Vous pouvez [en lire davantage ici (MDN).](https://developer.mozilla.org/fr/docs/Web/Guide/HTML/Formulaires/Envoyer_et_extraire_les_donn%C3%A9es_des_formulaires)

### <code>fieldset + legend</code>

`<fieldset>`permet de sectionner le formulaire en  regroupant plusieurs contrôles interactifs. Il est particulierement utile dans le cas de formulaire complèxes ou nous devons recuperer plusieurs type de donneés (personnelles, experience, mode de contact, etc.)

```html
<form>
  <fieldset>
    <legend>Données personnelles</legend>
    <!-- à venir -->
  </fieldset>
  <fieldset>
    <legend>Expérience web</legend>
    <!-- à venir -->
  </fieldset>
  <fieldset>
    <legend>Mode de contacte</legend>
     <!-- à venir -->
  </fieldset>
</form>
```

![](https://wptemplates.pehaa.com/assets/alyra/fieldset.png)

## Contrôle interactif - <code>input</input>

L'élément vide `<input>` crée un contrôle interactif. Les saisies possibles et son comportement dépend fortement de la valeur indiquée par son attribut `type`.

```html
<input type="email" id="email" name="email" required />
```

Regardons les attributs souvent utilisé avec `input`

- `type` - par défaut text



### <code>input</code> type text et email

Chaque contrôle interactif (`input`) est accompagné par son élément qui le décrit [`label`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/label). Pour que la liason fonctionne l'attribut `for` de `<label>` doit correspondre à l'attribut `id` de `input`.

```html
<label for="user-name">Votre nom</label>
<input id="user-name" name="user-name" type="text" />
```

et un autre exemple 

```html
<label for="user-email">Votre e-mail</label>
<input id="user-email" name="user-email" type="email" />
```

![](https://wptemplates.pehaa.com/assets/alyra/labelinput.png)



mettre ne place - [basé sur ce pen](https://codepen.io/alyra/pen/qBOzGRo)

## Exercices

- [Monstre](https://codepen.io/alyra/pen/LYpJrwg) | [solution](https://codepen.io/alyra/pen/6476cabbc1a5a1849f5bb349a4fa4ea0)
- [Form - Dev Freelance](https://codepen.io/alyra/pen/pojOZoP) | [solution](https://codepen.io/alyra/pen/6614f36dcfcc8ae7045f250135dc77e8)
