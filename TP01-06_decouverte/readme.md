# [TD1/6] Découverte du langage HTML et CSS
HTML est un héros et CSS est son acolyte, un peu comme Batman et Robin. Tout comme l'homme chauve-souris, HTML n'a pas besoin de CSS pour fonctionner. Par exemple :
http://motherfuckingwebsite.com/
Malgré l'absence de code CSS, le site reste consultable.
Par contre, pour un fichier CSS, sa vie n'a aucun sens s'il n'est pas en couple avec un fichier HTML.
## Découverte d'HTML
### Son rôle
HTML (HyperText Markup Language) est un langage de balisage qui permet de structurer les informations d'un document web. Il est généralement destiné à être lu par un navigateur pour formater correctement le texte.
Il est aussi parcouru par des robots pour indexer une page sur les moteurs de recherche ou par des assistants pour les personnes atteintes d'un handicap qui les empêches d'utiliser un écran.
Bien choisir les balises quand on structure un document permet d'améliorer sa compréhension par les bots de Google, les assistants vocaux et même par vous lorsque vous relirez votre code.
### La structure d'un document HTML
```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <!-- Information sur la page -->
</head>

<body>
  <!-- Contenu de la page-->

</body>
</html>
```
- `doctype` définit le type du document.
- `<html>` marque le début et la fin du document. Remarquez également l'attribut `lang="fr"` qui permet à un assistant vocal de lire correctement les textes (par exemple : les accents)
- `<head>` inclut les informations sur la page comme son titre, sa description. C'est là où l'on place d'autres métadonnées comme les liens vers les ressources CSS et Javascript, la favicon, le comportement en responsive, …
- `body` corresponds à la partie visible du document, là où le contenu de la page sera visible pour les utilisateurs.
### Liste et définitions des éléments HTML
[https://web.iamvdo.me/html/balises/](https://web.iamvdo.me/html/balises/)
### Vocabulaire à connaitre
- Un `id` est un identifiant. Il doit être unique dans la page parce qu'il sert de repère pour aller directement à une section du document. Il se créée avec la syntaxe`<p id="nom-id">` et on le lie avec un lien `<a href="#mon-id">`.
- Une `class` est une spécificité pour le CSS. Elle permet de créer une ou plusieurs « étiquette(s) », ce qui permet d'appliquer la même mise en forme à tous les éléments qui partage le même nom de classe. On déclare une classe comme ceci : `<p class="class autre-class class-trois">`. Le nom d'une classe ne peut pas commencer par un chiffre.
- Les attributs (`attr`) permettent de donner une information complémentaire (l'adresse d'un lien avec `href`) ou le comportement par défaut d'un élément comme `autoplay` pour une vidéo
###

### Son rôle
CSS (Cascade Style Sheet) est un langage de présentation qui permet aux navigateurs de comprendre comment mettre en page un document HTML. Un fichier CSS s'appelle dans le HTML de cette manière
````html
<link rel="stylesheet" media="screen" href="chemin/nom-du-fichier.css" >
````
La convention actuelle est de nommer son fichier css `style.css`. L'attribut `media` existe parce que CSS n'est pas uniquement destiné aux écrans. On peut aussi styler un document pour son rendu en impression par exemple.
### Déclaration d'une règle CSS
````CSS
sélecteur {propriété: valeur;}
````
- Un sélecteur sert à déclarer aux navigateurs pour quels éléments il doit appliquer ce style.
- Une propriété est le nom de la propriété que l'on souhaite changer (taille de police par exemple).
- La valeur est la nouvelle valeur que le navigateur doit appliquer (18px)
 #### Exemple :
````CSS
p {color: blue}
````
Avec cette règle, tous les paragraphes `<p>` du site seront colorés en bleu. Pour les `id`, les `class`, et les `attributs`, le sélecteur porte cette syntaxe :
````CSS
#id {}
.classe {}
[attr="nom-attribut"]
````
### La relation parent / enfant
Comment faire pour styler tous les liens `<a>` uniquement lorsqu'ils sont dans un paragraphe `<p>` ? Pour résoudre ce problème, le concept de parentalité entre dans le game. Par exemple :
````HTML
<p>je suis un paragraphe qui contient <a href="https://google.com">un lien vers google</a>
````
Le lien se trouve à l'intérieur du paragraphe donc `<p>` devient le parent du `<a>` qu'il héberge.
Donc pour styler les liens dans les `<p>`, le CSS s'écrit de cette façon :
`````CSS
p a {font-weight: bold}
``````
À partir de maintenant, tous les liens qui se trouve dans une balise `<p>` seront en gras.
### Une même règle pour plusieurs sélecteurs ?
Pour styler plusieurs éléments de la même manière, on sépare les sélecteurs par une virgule.
``````CSS
h1,h2,h3,
h4,h5,h6 {font-family : "Nom de la police"}
``````
### CSS et le poids des ~~mots~~ sélecteurs
Pour départager deux styles différents pour un même sélecteur, le navigateur va vérifier deux choses :
- Quel sélecteur a le plus de poids
- Et si le poids est égal, il va sélectionner le style qu'il a trouvé en dernier.

Pour peser des sélecteurs, le navigateur leur applique les scores suivants : +100 points pour les `#id`, +10 points pour les `.class`, attributs `[attr]` et pseudo-classes et 1 point pour les éléments (ex: `p`) et pseudos-éléments. Ce poids porte le nom de **spécificité**
Pour mieux comprendre la spécificité CSS ➡ [calculette de spécificité](https://specificity.keegan.st/)

### Pseudo-classes
Une pseudo-classe est une expression qu'on attache à un sélecteur pour le styler dans un contexte plus spécifique. Par exemple, je peux avoir besoin de changer la couleur d'un lien quand je le survole ; où bien agrandir la taille du premier paragraphe se trouvant dans une balise `<article>` sans toucher aux autres. Voici quelques exemples :
````CSS
/* change la couleur quand je survole un lien */
a:hover {color:#fb1}

/*
   Change la couleur de bordure d'un textarea quand il est sélectionné
   par le clavier (TAB) ou par la souris
*/
textarea:focus {border-color: red}

/*
  Change la taille d'un <p> uniquement s'il est le premier enfant de son parent.
  Donc ici :
  <article>
    <h1>titre</h1>
    <p>texte</p>
  </article>
  ne fonctionnera pas parce que <p> est le deuxième enfant de <article>
*/
p:first-child {font-size: 20px}

/*
  Change la taille d'un <p> uniquement s'il est le dernier enfant de son parent.
  Donc la même règle s'applique que pour first-child
*/
p:last-child
````
👉 [La liste de toutes les pseudo-classes](https://developer.mozilla.org/fr/docs/Web/CSS/Pseudo-classes). Les plus utiles sont celles qui contiennent un « child » ou « not » pour cibler plus précisément. « hover », « focus » et « active » sont utiles pour styler les réactions — appelé « micro-interaction » —quand l'utilisateur agit sur un élément.

### Pseudo-éléments
Les pseudo-éléments servent à styler une fraction d'un élément comme sa première lettre par exemple. Ils servent aussi à créer des éléments virtuels qui n'apparaissent pas dans le HTML afin de bien séparer le contenu de sa forme.
#### Exemple de pseudo-élément
`````CSS
/*Pseudo élément pour styler une fraction d'un élément*/
p:first-letter {font-size: 22px};
p:first-line {color: ~#bada55;}

/* Pseudo élément pour créer des éléments virtuels*/
/* Injecte "coucou" avant le texte <p>*/
p:before {content:"coucou"}
/* Injecte "coucou" après le texte <p> */
p:before {content:"beuh !!"}
`````
👉 [La liste de tous les pseudo-éléments](https://developer.mozilla.org/fr/docs/Web/CSS/Pseudo-%C3%A9l%C3%A9ments). Les plus utiles sont `before` et `after`. `placeholder` est aussi utile pour mieux styler les formulaires.

### Appeler un fichier avec CSS
Pour dire au navigateur d'aller chercher une image d'arrière-plan par exemple, on déclare utilise `url("chemin/fichier.jpg")` :
`````CSS
sélecteur {background-image: url("chemin/fichier.jpg")}
``````
## HTML et CSS, chacun son business
Il est important de comprendre qu'HTML sert pour livrer du contenu et CSS pour dire comment le présenter. On ne se préoccupe jamais du rendu d'un texte dans le HTML. Un texte tout en capitales doit être fait avec CSS par exemple. Un texte en gras doit être une information importante. Si c'est pour le style, alors c'est CSS qui doit gérer ça.

# Travaux pratiques
## Challenge HTML
- [ ] Créez votre propre copie HTML de l'article suivant : [« L’ergonomie des claviers ou quand confort rime avec santé ! »](https://docs.google.com/document/d/1yGe2Ye3cpWDDAssYb4muYPHnUpWCnczMJ6L4u79FJyc/edit?usp=sharing) | [Source origiale de l\'article](https://www.24joursdeweb.fr/2019/ergonomie-claviers/). 👉 Attention à bien faire attention à la sémantique. Vous devez également intégrer le plan de l'article avec les liens qui pointent vers la bonne section de l'article section. Les textes en gris sont les légendes des images.
### Rappel de la structure d'un HTML
```` HTML
<!DOCTYPE html>
  <html lang="fr">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title></title>
    </head>
  <body>

  </body>
</html>
````
## Challenge CSS
Une fois l'article intégré, achevez cette checklist :
- [ ] `html` et `body`, `box-sizing: border-box` (notion qu'on découvrira plus tard)
- [ ] Article, taille maximum de 800 pixels et centrer.
- [ ] Article, marge interne de 32 pixels sur les côtés.
- [ ] Le premier paragraphe de l'article en noir et 20 pixels
- [ ] L'article, taille de police 18 pixels
- [ ] Les liens en bleus et devienne de couleur `tomato` quand je survole ou quand il est sélectionné avec mon clavier.
- [ ] Images, ombre portée de 10 pixels en `rgba(0,0,0,.3)`
- [ ] Je veux 5 éléments de couleur rouge mais cela ne doit pas être la même balise. Vous pouvez encapsuler du texte dans une balise `<span>` si vous voulez.
- [ ] À la fin de l'article, intégrez un formulaire pour commenter l'article. Les champs requis sont pseudo (input texte), email (input texte), commentaire (zone de texte). Ils sont tous obligatoires. Le formulaire ne doit pas être fonctionnel.
