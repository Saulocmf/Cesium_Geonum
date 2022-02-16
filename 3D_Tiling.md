### *[3D Tiling](https://cesium.com/learn/3d-tiling/)*
<div align="justify">
Les 3D Tiles ont été créés suite à une initiative de Césium et correspondent à un modèle de données facilitant le travail, l’analyse, le partage et la diffusion des données 3D. 
<img align="right" src="/Figures/3D_Tiles.png">

Grâce au format 3D Tiles, plusieurs formats de données 3D (qui sont parfois très lourds) peuvent être combinés dans un seul jeu de données avec un format gITF.




Pour résumer leur fonctionnement, un ensemble de données provenant de différentes sources peut être regroupé et combiné dans un seul jeu de données 3D Tiles au format gITF. Ce jeu de données 3D Tiles permet d’optimiser le partage et la diffusion des données mais est aussi intéractif, libre, personnalisable, adaptable, flexible, durable …

Au sein de Césium, les 3D tiles sont utilisables aussi bien dans Césium Ion que dans Césium.js. Des 3D tiles sont par ailleurs déjà mises à disposition par Césium.
Les formats de données acceptés pour former des 3D Tiles sont multiples et dépendent des domaines d’applications. On peut par exemple citer les formats CityGML et KML pour la construction de modèle 3D de bâtiments ; les formats Filmbox, gITF, Wavefront OBJ … pour les modèles BIM et CAD ; les formats GeoTIFF, ASCII, JPEG, PNG … pour l’imagerie et la photogrammétrie ; ou encore LAS et LAZ pour les données Lidar.

### Tutoriel : Utiliser la plateforme Césium Ion pour ajouter des données 3D

L’insertion des données 3D dans l’espace de stockage de Césium se déroule comme suit. En se rendant sur la plateforme, nous arrivons sur l’interface suivante (présentée sur la figure ci-dessous) : au milieu se trouve une liste comprenant l’ensemble des données que nous avons ajouté précédemment à notre espace, avec leur caractéristiques. Un panneau sur la droite permet de visualiser chacune des données sur un globe terrestre. A noter qu’il est possible d’accéder à des données fournies par Césium à partir de la barre de recherche et que les stories sont accessibles dans le premier onglet en haut à gauche.

<p align="center">
  <img align="center" src="/Figures/MyAssets.png">
</p>


Cliquer sur “Add data” pour ajouter nos propres données. Ici, nous allons ajouter les données 3D des bâtiments du 2e arrondissement de Lyon, au format GML. Comme expliqué précédemment, Césium prend en charge un certain nombre de formats 3D, et ceux-ci sont séparés dans en deux catégories : “3D Tiles” (se visualisant avec un carré autour) et “KML, CZML, or GEOJson”. Dans notre cas, nous allons insérer les données en tant que 3D Tiles. Le fichier principal JSON se sélectionne naturellement si aucun autre fichier du même type, pouvant prêter à confusion, est présent.

<p align="center">
  <img align="center" src="/Figures/AddData.png">
</p>

Après quelques secondes d’attente, le modèle est ajouté à notre espace et est ici visualisable. <img align="right" width="300" src="/GIF/gif_overview.gif"> 
Un bout de code est également rendu disponible pour faciliter l’insertion des données avec Cesium.js. Le code fait appel au type de données et à son identifiant, créé à l’insertion des données dans notre espace. 

<p align="center">
  <img align="center" src="/Figures/Code.png">
</p>

Malheureusement, les données de Lyon ne contenant pas de données attributaires ni de style image disponible, nous ne pourrons pas les utiliser dans les parties suivantes et utiliserons des données fournies par Césium.

  
<p align="center">
  <img align="center" src="/GIF/tuto_assets_recadre.gif">
</p>
  
  
</div>
