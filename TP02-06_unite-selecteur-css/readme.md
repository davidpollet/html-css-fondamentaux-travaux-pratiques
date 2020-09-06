# [TD2/6] CSS kickstart
## CSS Box Model
``````CSS
.box {
  width: 500px;
  border: 10px solid green;
  padding: 10px;
}
``````
À votre avis, quelle est la largeur réelle de l'élément ? Les paddings et les bordures se soustraient ou s'ajoutent à la `width` de 500 pixels ?
C'est précisement à cette question que le box model doit répondre. Il se déclare avec la propriété `box-sizing` et permet de dire au navigateur comment il doit calculer la taille d'un élément.
