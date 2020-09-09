# [TD2/6] CSS kickstart
## CSS Box Model
``````CSS
*,
*:before,
*:after {
  box-sizing: border-box;
}

.box {
  background: #fb1;
  border-right: 10px solid black;
  padding-right: 10px;
  width: 500px;
}
``````
À votre avis, quelle est la largeur réelle de l'élément ? Les paddings et les bordures se soustraient ou s'ajoutent au `width` de 500 pixels ?
C'est précisément à cette question que le box model doit répondre. Il se déclare avec la propriété `box-sizing` et permet de dire au navigateur comment il doit calculer la taille d'un élément.
![Illutration qui montre la différence entre les deux valeurs de box-sizing. En content-box, les paddings et les widths sont ajoutés à la taille de la boite. En border-box, ils sont soustraits](img/css-box-model.gif)
Comme on le voit sur l'illustration, `border-box` offre plus de confort parce que cela nous évite de devoir faire des calculs pour éviter de tout casser. La valeur par défaut des navigateurs est `content-box` donc on devra appliquer le code suivant :
``````CSS
*,
*:before,
*:after {
  box-sizing: border-box;
}
``````
### Pourquoi `border-box` n'est pas la valeur par défaut ?
Parce que la philosophie des navigateurs est d'être rétro-compatible. Changer la valeur par défaut signifierait casser des millions de sites qui ont été intégré quand `box-sizing` n'existait pas.

## Les sélecteurs CSS
Dans la première semaine, on a vu que pour styler un élément HTML, une règle CSS prend cette syntaxe :
```````CSS
sélecteur {propriété: valeur}
````````
Pour sélectionner tous les éléments, on utilise le symbole `*` :
``````CSS
* {margin: 0}
``````
On peut imbriquer les sélecteurs pour être plus précis et styler un élément dans un contexte bien défini :
``````CSS
li a {color: green}
``````
Dans le code ci-dessus, on demande de styler les liens uniquement lorsqu'ils sont dans des éléments de liste.
### Passez en mode sniper
Au delà de la sélection pure, il existe des outils qui nous permettent d'affiner davantage notre ciblage. Par exemple :
``````HTML
<li>
  <p>
    <a href="">mon lien</a>
  </p>
<li>
``````
Ici, selon le CSS déclaré au-dessus, mes liens seront en vert parce que le navigateur aura trouvé un `<a>` dans un `<li>`. Comment faire pour empêcher ce comportement ? Avec un sélecteur d'enfant direct.
### Sélecteur d'enfant direct
``````CSS
li > a {color: green}
``````
Le chevron qui s'est incrusté entre `li` et `a` permet de dire :
> « Cher navigateur, style les liens dans les `li` en vert uniquement quand il y a rien entre les deux. Bisous. »

Ici,
``````HTML
<li>
  <p>
    <a href="">mon lien</a>
  </p>
<li>
``````
Les liens ne seront pas colorés en vert parce qu'il y a un `<p>` entre les deux. Par contre,
``````HTML
<li>
  <a href="">mon lien</a>
<li>
``````
Là, le style sera appliqué parce qu'il n'y a rien entre les deux éléments.
#### Les autres sélecteurs avancés
Plutôt que de vous détailler chaque sélecteur comme au-dessus et d'avoir des décès d'ennuis sur la conscience, je vous propose de jouer à [CSS Diner](https://flukeout.github.io/) qui vous donnera les clés pour être à l'aise avec la plupart des sélecteurs.

## Les unités CSS
Pour pouvoir dimensionner, CSS offre toute une panoplie d'unité de mesure qui peuvent répondre à un besoin précis selon les cas.
### Causons accessibilité avant
Excepté dans quelques cas exotique, il y a un consensus pour que la valeur par défaut de `font-size` soit de 16 pixels.
Par contre, si je suis déficient visuel ou que mon écran se trouve loin (comme une TV), je peux aller dans mes paramètres de mon navigateur et agrandir la taille de police par défaut. Et si je m'embête à faire ces réglages, j'aimerai bien qu'ils soient appliqués partout. Donc c'est à l'intégrateur de faire le job pour que ce soit le cas.
### pixel
``````CSS
p { font-size: 16px}
``````
 - 👍 Simple à déclarer
 - 👎 Unité fixe. Le navigateur n'agrandit pas le texte donc vous ne respectez pas les préférences des utilisateurs (HONTE À VOUS)
### em
Le `em` est une unité relative à la taille déclarée sur le parent. Sa valeur en pixel est calculée par multiplication :
![Illustration d\'un calcul d\'une valeur en em](img/unite-css-em.gif)
 - 👍 Unité relative donc elle respecte les préférences utilisateurs
 - 👎 Peut vite devenir complexe comme sur le `<p>` de l'exemple où 3 multiplications sont nécessaires pour obtenir va valeur en pixels. Beaucoup trop de calvities sont apparues à cause de ça.
 ### rem, le meilleur des mondes
 Le rem est apparu pour gommer le défaut de `em` en se référant uniquement à la racine du document : le `font-size` de l'élément `html` s'il a été changé, ou le `font-size` défini par le navigateur.
 ![Illustration d\'un calcul d\'une valeur en em](img/unite-css-rem.gif)
  - 👍 Unité relative
  - 👍 Une seule opération à faire pour prédire sa conversion en pixel.
### vw, vh
Les deux dernières unités à connaitre pour couvrir la plupart des cas de figure sont les unités relatives au viewport. Le viewport est la taille disponible sur votre écran pour afficher le contenu de la page. `vw` est pour « viewport width », et `vh` pour « viewport heigth ».
![Illustration des unités Viewport Units](img/css-viewport-unit.png)
## Le positionnement
Pour déplacer un élément de son emplacement d'origine, on va modifier sa position via la propriété … `position`
### Position relative
La position relative déplace un élément depuis son emplacement d'origine.
![ ](img/css-position-relative.gif)
Remarquez que la place que l'image occupait avant son déplacement est toujours reservée.
### Position absolute : qui va à la chasse perd sa place
Un élément avec une `position: absolue` se positionne par rapport au premier parent en position relative ou sinon, par rapport à la fenêtre.
![ ](img/css-position-absolute.gif)
Dès qu'on déclare une position absolue, l'élément perd son emplacement et ses frères viennent occuper l'espace laissé libre. On dit qu'il sort du flux.
### Position fixed
Une position avec une valeur `fixed` permet de coller un élément à un endroit de la fenêtre. Elle aura toujours pour origine la fenêtre.
![ ](img/css-position-fixed.gif)
De la même manière que pour la position absolute, le navigateur lui retire la place qui lui était réservé dans le flux.
### Z-index
Quand plusieurs éléments se chevauche, comment dire au navigateur quel élément doit passer au-dessus ? C'est là que la propriété `z-index` intervient.
![ ](img/z-index.gif)
Si la valeur de `z-index` est supérieure et a une position autre que `static`, l'élément passera au-dessus.
__Attention__
``````CSS
.box {position: relative}
.box:nth-child(1) {z-index: 1;}
.box:nth-child(2) {z-index: 2;}

.box:nth-child(1) .child {
  position: relative;
  z-index: 3;
}
``````
Dans le code ci-dessus, on pourrait penser que `.child` va passer au-dessus de `box:nth-child(2)` parce qu'il a un `z-index` supérieur… Eh bien non. Si son parent a un z-index inférieur, il restera en dessous parce que le z-index est comparé d'abord avec la valeur de ses frères. C'est ce qu'on appelle le contexte d'empilement.

## Le responsive design
Le responsive design est la solution pour pouvoir adapter une interface web à n'importe quelle taille d'écran. Cette solution est dépendante du viewport.
### Le viewport
Le viewport est la place disponible pour afficher le contenu. Avant l'invention de la balise `<meta name="viewport">`, un site web se comportaient comme une image : il se réduisait jusqu'à ce qu'il rentre entièrement dans la zone d'affichage
![ ](img/meta-viewport.png)
Avec un viewport `width=device-width, initial-scale=1.0`, l'écran est forcé d'utilisé sa taille réelle et la consultation devient possible sans zoomer / dézoomer son écran.
### Les media queries
Pour changer la mise en page d'un site à partir d'une taille définie :
``````CSS
@media screen and (min-width: 600px) {
  body {
    font-size: 1.125rem;
  }
}
``````
Dès qu'une fenêtre aura 600 pixels disponible en largeur, la taille de police de `body` passera à `1.125rem` (18 pixels dans un contexte standard). La valeur de `min-width` est appelé _breakpoint_.
#### Mobile-first vs Desktop-first
Il y a deux approches quand on intègre un site responsive : Avec le mobile-first, on commence par déclarer sa mise en page pour les mobile, puis on modifie la mise en page au fur-et-à-mesure que la place disponible augmente.
Le desktop-first, c'est l'inverse. On part du plus grand pour arriver au plus petit.
##### Pourquoi le _mobile-first_ est une meilleure approche ?
Les conteneurs HTML de type _bloc_ ont une largeur par défaut de 100% et c'est ce qu'on veut sur mobile, faute de place. Les éléments autours du contenu sur un grand écran ne peuvent pas l'être sur mobile. Tout cela fait qu'en _desktop-first_, on doit produire du code inutile pour réadapter la mise en page
![ ](img/mobile-first-desktop-first.png)
Comme `main` a une taille par défaut de 100% et un `font-size` de 1em, il est inutile de le déclarer pour les mobiles. Le code est plus léger. Maintenant, il est possible que dans certains cas, une approche desktop fist soit plus approprié. __Le plus important est de savoir ce qu'on fait et pourquoi on le fait.__
__Il est important de noter que le responsive n'est pas unidirectionnel.__  Un design peut être adapté en fonction de la hauteur de fenêtre disponible.
Notez aussi qu'on peut déclarer plusieurs conditions :
``````CSS
@media screen and (min-width: 600px) and (max-width: 800px) {
  body {
    background: yellow;
  }
}
``````
Ici, `body` changera sa couleur d'arrière-plan en jaune quand la largeur fenêtre sera comprise entre 600 et 800 pixels.
## Vérifier la compatibilité des nouvelles fonctionnalités
Les langages web évoluent avec le temps. Pour utiliser une nouvelle fonctionnalité, on doit s'assurer qu'elle soit compatible avec les navigateurs que l'on vise. La référence dans ce domaine est [Can I Use ?](caniuse.com/).
## Travaux pratiques
➡ [Accéder aux challenges](./challenge.html) (clic droit -> enregistrez-sous.)
