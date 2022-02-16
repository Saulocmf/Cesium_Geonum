### *[Cesium JS](https://cesium.com/learn/cesiumjs-learn/)*
<div align="justify">
L’outil Césium JS est une librairie Javascript open source permettant d’intégrer et de visualiser des objets 3D dans des applications web. Grâce à Césium JS, il suffit de choisir les objets ou éléments à modéliser et le script correspondant est donné. Il est ensuite possible de l’ajouter à son script et de modifier les différents paramètres pour le personnaliser.
Cette librairie offre un très grand nombre de fonctions permettant de travailler, d’analyser et de styliser les données 3D. Il est par exemple possible de styliser et des filtrer des couches 3D, de créer et de dessiner des entités dans l’espace (point, ligne, polygones, volumes, model…), de modifier l’apparence des objets, d’intégrer des images raster, d’ajouter des objets interactifs (voitures, avions) ou encore d'ajouter des textures sur des bâtiments.
Le tutoriel présenté ci-après donne un exemple d’utilisation de cet outil pour insérer un bâtiment 3D dans l’espace.
  Note: Ce tutoriel a été inspiré du tutoriel original en anglais "Visualize a Proposed Building in a 3D City" disponible sur www.cesium.com.

### Tutoriel :  Insertion d’un modèle 3D de bâtiment(s) dans une ville et visualisation de son impact

En premier lieu, il est nécessaire de créer une clé API personnelle sur le site de Césium. Cette clé (ou Token) est un identifiant unique qui sera utilisé dans notre code pour qu’il soit validé par Cesium.
  
<p align="center">
<img align="center" height= 200 src="/Figures/Token.png">
</p>

Une fois en possession de ce Token, nous avons deux choix pour le développement :
######  - Utiliser notre propre application installée pour coder et avoir les fichiers dans notre propre ordinateur (Visual studio, Notepad++…) 
######  - Créer un projet sur le site web [Glitch](www.glitch.com) où tout sera fait en ligne.
Quelque soit l’option choisie, la prochaine étape est la même dans les deux cas et permet d’insérer dans un fichier Index.html les codes de base html et le token d’accès personnel. Il est également nécessaire de créer les fichiers auxiliaire css, js et json si ce n’est pas encore fait, et de lier ces fichiers au fichier HTML de manière habituelle.
Après avoir mis en place le projet, les étapes sont les suivantes :

  
* Étape 1 : Initiation du projet avec l’import de la librairie
  
Pour cela, dans la balise <script>, il est nécessaire d’insérer la librairie Césium.js, comme suit.
```
<!DOCTYPE html>
<head>
  <script src="https://cesium.com/downloads/cesiumjs/releases/1.89/Build/Cesium/Cesium.js"></script>
  <link href="https://cesium.com/downloads/cesiumjs/releases/1.89/Build/Cesium/Widgets/widgets.css" rel="stylesheet">
  <link href="style.css" rel="stylesheet">
</head>
<body>
  <div id="cesiumContainer"></div>
   <script>
   </script>
</body>
</html>
```
Dans le fichier Javascript, insérer le token Césium créé précédemment :
```
Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI5Y2RiMDVmNC1iN2Q0LTQzMzYtOTlmNS00YjUwZjZmNmEyMTUiLCJpZCI6ODAyMjAsImlhdCI6MTY0MjY4NDg5Nn0.XpOeBkCnOLRxBbo5r7KbVyEjycVMzNlZuWkwtCrkGzs';
```
  
* Étape 2 : Ajouter une couche de bâtiments et plan de fond de relief
Ajouter d’abord un plan de fond de terrain Césium grâce à Césium Viewer.
```
const viewer = new Cesium.Viewer('cesiumContainer', {terrainProvider: Cesium.createWorldTerrain()});
```
Ensuite, dans notre cas, insérer la couche des bâtiments OSM Césium, mais il est possible d’ajouter vos propres bâtiments à ce moment :
```
const buildingsTileset = viewer.scene.primitives.add(Cesium.createOsmBuildings());
```
Zoomer sur le point de votre choix (où se situe vos données) en indiquant dans l’ordre le couple de coordonnées désiré puis le niveau de zoom souhaité.
```
viewer.camera.flyTo({ destination: Cesium.Cartesian3.fromDegrees(-104.9965, 39.74248, 4000)});
```

Après avoir réalisé les deux étapes précédentes, le résultat ressemble au suivant :
<p align="center">
<img align="center" title="jcjf" src="/Figures/BatimentJS.png">
</p>
  
* Étape 3 : Définir la localisation de l’emprise au sol du bâtiment à styliser
  
Avant d’ajouter le nouveau bâtiment nous devons ajouter une couche geojson qui marque son emprise au sol. Cette étape permet de repérer les bâtiments existants qui devront être retirés de la zone. Si ce n’est pas encore fait, c’est le moment de charger votre fichier geojson correspondant à l’emprise au sol du bâtiment dans votre espace Césium Ion, selon le tutoriel décrit en première partie.
  
* Étape 4 :  Ajouter l’emprise au sol dans le modèle
  
L’action précédente attribuera un code ID pour la couche geojson ajoutée sur Césium (en bas et à droite de la fenêtre de visualisation). Pour ajouter l’objet, il faut insérer son code ID dans le script en remplaçant le texte «numero_emprise» par ce numéro. Cette méthode d’insertion de fichier 3D est la même pour toutes les couches insérées dans Césium Ion, quel que soit leur type.
```
async function addBuildingGeoJSON() {
// Charger le fichier GEOJSON depuis Césium Ion
  const geoJSONURL = await Cesium.IonResource.fromAssetId(numero_emprise);
// Définir le nouveau fichier en temps que géométrie, et placer cette géométrie sur le sol
  const geoJSON = await Cesium.GeoJsonDataSource.load(geoJSONURL, { clampToGround: true });
// Ajouter la couche de base des batiments 3D à la visualisation
  const bati_base = await viewer.dataSources.add(geoJSON);
// Zoomer sur le nouveau polygone
  viewer.flyTo(bati_base);
}
addBuildingGeoJSON();
```
Cela permettra de repérer l’emprise du bâtiment au sol :
<p align="center">
<img align="center" height= 250 src="/Figures/Emprisesol.png">
</p>
  
* Étape 5 : Style et gestion des bâtiments alentours
À partir de l’emprise au sol, il est possible voir que sur le terrain, quelques bâtiments sont présents dans la zone choisie où l’on veut placer le nouveau bâtiment :
  
<p align="center">
<img align="center" height= 250 src="/Figures/Batiment.png">
</p>
  
Le script suivant permet de « cacher » ou simplement ne pas afficher ces bâtiments existants. Pour cela, on crée une condition au sein du paramètre “show”, qui permet normalement d’afficher ou non la couche entière. Dans notre cas, puisque seuls certains bâtiments ne sont pas à visualiser, nous allons récupérer leur identifiant (via un clic sur le modèle), et créer une condition pour chacun d’entre eux du type “si tel bâtiment correspond à tel identifiant, alors on ne l’affiche pas”. ${elementId} se réfère au champ attributaire de la 3D tile et “false” indique que le bâtiment correspondant ne sera pas affiché. Tous les autres bâtiments ont pour paramètre “true” et s’affichent.

```
// Masquer certains bâtiments dans la zone
buildingsTileset.style = new Cesium.Cesium3DTileStyle({
// Création d’une règle au sein du paramètre “show” de la couche
  show: {
    conditions : [
      ['${elementId} === 332469316', false],
      ['${elementId} === 332469317', false],
      ['${elementId} === 235368665', false],
      ['${elementId} === 530288180', false],
      ['${elementId} === 530288179', false],
      ['${elementId} === 532245203', false],
// Affichage de tous les autres bâtiments
      [true, true]
    ]
  },
// Appliquer une couleur basée sur les attributs de la couche
  color: "Boolean(${feature['cesium#color']}) ? color(${feature['cesium#color']}) : color('#ffffff')"
});
```
Comme visible ci-dessus, il est alors possible d'assigner une couleur à chaque bâtiment en fonction de l'un de ses attributs : ici, l'attribut "cesium#color" fait d'abord appel à une fonction Booléenne pour définir si l'attribut contient une valeur. Si oui, la couleur sera assignée au bâtiment (via "color($(feature['cesium#color']))", color faisant référence à la fonction qui gère les couleurs dans Césium.js, feature faisant appel à l'attribut). Dans le cas inverse, les bâtiments seront colorés en blanc grâce au code couleur "#ffffff".

* Étape 6 : Ajouter le modèle 3D du bâtiment dans Césium Ion

C’est maintenant le moment d’insérer le modèle 3D de votre/vos bâtiment(s) dans Césium Ion. Pour cela, reprenez les étapes décrites dans le tutoriel de la seconde partie. Une fois cette étape effectuée, il est nécessaire de choisir “Adjust Tileset Location” au dessus de la fenêtre d’affichage de la couche. Pour paramétrer l’insertion du bâtiment correctement, il est important de suivre les étapes suivantes, toujours dans Césium Ion.
######  - Cliquer sur « zoom to tileset »
######  - Insérer les paramètres de localisation de votre bâtiment qui comprennent la longitude, la latitude, la hauteur du bâtiment et son “heading”. 
######  - Cliquer sur « Save »
Pour plus de détails sur les formats de modèles 3D tiles acceptés par Césium Ion, se référer à la première partie de cette documentation. 

* Étape 7 : Ajouter le modèle 3D du bâtiment 
  
Pour ajouter le modèle 3D du nouveau bâtiment, remplacer “identifiant_batiment” par l’identifiant fourni par Césium Ion dans le script ci-dessous. Il est ici nécessaire de préciser qu’il s’agit d’un “3DTileset” à l’intérieur de la constante créée afin que Césium.js le reconnaisse comme tel. La ligne située après “url” est ensuite au même format que pour le fichier GeoJSON inséré plus tôt dans le tutoriel.

```  
const nouveau_bati = viewer.scene.primitives.add(
  new Cesium.Cesium3DTileset({
    url: Cesium.IonResource.fromAssetId(identifiant_batiment)
  })
);
// Déplacer la vue 
viewer.flyTo(nouveau_bati);
```
  
Nous utiliserons ensuite la fonction “flyTo” du Viewer afin de ramener la vue sur le bâtiment nouvellement inséré.
<p align="center">
<img align="center" src="/Figures/Modele3D.png">
</p>  
  
* BONUS : Gérer l’affichage du bâtiment
Il est ensuite possible d’ajouter un contrôle pour gérer l’affichage ou non du nouveau bâtiment.
Dans le fichier index.html, ajouter un bouton permettant d’afficher ou non le bâtiment, dans la partie <body> :
```  
<button id="afficher-bati">Afficher le nouveau batiment</button>
```  
Puis ajouter un style CSS à ce bouton, comme suit, soit dans le fichier HTML sous la balise <style>, ou directement dans votre fichier CSS.
```  
<style type="text/css">
#afficher-bati { z-index: 2; position: absolute; top: 7px; left: 7px}
</style>
```  
Enfin, ajouter le code suivants dans le fichier Javascript pour faire fonctionner le bouton. “querySelector” permet de sélectionner l’élément à animer, pendant que “onclick” définit l’action pour déclencher l’animation. Une fonction est ensuite créée pour définir l’animation en question, ici avec “show”.
```  
// Afficher le bâtiment au clic du bouton
document.querySelector('#afficher-bati').onclick = function() {
  nouveau_bati.show = !nouveau_bati.show;
};
```  
  
* Étape 9 – Visualisez et évaluez l’impact du nouveau bâtiment aux alentours
  
Vous pouvez comparer la scène avec ou sans la nouvelle construction dans le contexte de l’horizon de la ville et des autres bâtiments. Appuyez sur le bouton « afficher bâti» pour afficher ou masquer le modèle 3D.

<p align="center">
<img align="center" src="/Figures/RenduFinal.png">
</p>    
  
  
  
  
  
  
  
  
  
  
  
  
  
</div>
