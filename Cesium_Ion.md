### *[Cesium Ion](https://cesium.com/learn/ion/)*
<div align="justify">
Césium Ion est une plateforme de modélisation, stylisation et de stockage de données 3D. Cette plateforme, dont les outils sont repris dans sa version Javascript, Cesium.js (de manière plus développée), est une application web interactive pour la visualisation de données 3D déjà existantes. Il n’est ainsi pas possible de créer des données 3D depuis l’application, comme il serait le cas dans la solution orientée développement, décrite par la suite. Si certaines données sont fournies par le service à l’inscription, il est possible de charger ses propres données, comme décrit dans la partie précédente. La principale force de Césium Ion repose sur ses « stories », permettant de combiner plusieurs visualisations dans un même document interactif à faire défiler (à la manière des stories Arcgis Online, ou Flourish). 
L’un des principaux avantages de Césium Ion est son intégration possible dans un large panel de logiciels tiers. En effet, les outils de Césium Ion sont principalement utilisables (et utilisés) dans les logiciels libres de modélisation et d’animation 3D Autodesk, Blender, FME, STK et WebODM. D’autres logiciels de modélisation 3D bien connus sont aussi capables de supporter les outils Césium, comme Metashape ou encore Sketchup, bien que plus rarement utilisés au sein de ces applications déjà fort complètes. A noter qu’un export de données 3D depuis ces logiciels vers l’espace de stockage de Césium est également disponible.

### Tutoriel : Utiliser la plateforme Césium Ion pour styliser les données 3D et créer des stories
Cette section présente un tutoriel de création et de stylisation d’une story. Pour ce faire, il n’y a pas besoin de connaissances en code, à l’inverse des visualisations de cesium.js, développées plus tard dans ce document. 

  
* Étape 1 : Ajouter les données 3D dans une story

Pour commencer, il est nécessaire d’avoir des données 3D de photogrammétrie présent dans l’espace « My Assets » de la plateforme. Césium Ion en fournit, mais il est possible d’utiliser les nôtres en les chargeant. Une fois les données réunies, il faut créer une nouvelle story. Une fois la nouvelle story créée, il est important de supprimer les données présentes par défaut sur la carte, les bâtiments OSM, et d’ajouter nos données via l’espace “Assets” en bas à gauche.
  
<p align="center">
<img align="center" src="/Figures/Batiments_OSM.png">
</p>
  
<br><br/>
  
* Étape 2 : Styliser des données 3D dans Césium Ion

Césium Ion permet également de styliser les données en fonction des attributs de la couche. Attention, cela n’est faisable que pour les données 3D ne possédant pas de photographies. Dans notre cas, nous utiliserons ici les données 3D de New York City fournies par Césium. Après les avoir importées comme décrit précédemment, nous pouvons passer à l’étape du style grâce au bouton «edit style» proposé à côté du nom de la couche. Dans cette partie, il est proposé de sélectionner n’importe quel attribut, comme sur un SIG, afin de le styliser. 

<p align="center">
<img align="center" src="/Figures/CreateStyle.png">
</p>

Ainsi, il est possible de catégoriser les bâtiments en fonction de leur type de propriétaire, en entrant les différents types dans les paramètres. On regrettera cependant l’absence d’une table de données, nous indiquant directement lesdits types. Il est cependant possible de cliquer sur chaque bâtiment et d’afficher ses attributs et valeurs, comme visible ci-dessous avec l’Empire State Building.

<p align="center">
<img align="center" src="/Figures/CategorizedStyle1.png">
</p>
  
<p align="center">
<img align="center" src="/Figures/CategorizedStyle2.png">
</p>
  
Il est également possible de créer un style gradué en fonction de valeurs numériques ou temporelles. Pour cela, après avoir sélectionné la valeur, il faut entrer une valeur minimale et maximale (éventuellement des intermédiaires) et sélectionner une palette pour visualiser les données. Ici, nous avons visualisé les bâtiments en fonction de leur année de construction.

<p align="center">
<img align="center" src="/Figures/GraduatedStyle.png">
</p>

<img align="right" src="/Figures/Styling.png">
<br><br/>
L’avantage de Césium Ion réside également dans le fait que la création d’un style n’efface pas les autres. En effet, un menu reprend l’ensemble des styles, qui se visualisent en sélectionnant la ligne en question. Il est donc aisé de réaliser des essais de styles différents et de les comparer. 
  
<br><br/>
  
* Étape 3 : Créer et interagir avec une story
  
Une fois les données ajoutées et stylisées, il est possible de créer une fenêtre de présentation («infobox») s’affichant par dessus la carte, et de réaliser une capture de la vue correspondant à notre positionnement.

<p align="center">
<img align="center" src="/Figures/Story1.png">
</p>
  
De plus, plusieurs outils sont disponibles pour analyser nos données visualisées. Dans le menu en bas de la fenêtre, il est possible de mesurer les bâtiments dans les dimensions X, Y et Z. 

<p align="center">
<img src="/Figures/Story2.png"> <img src="/Figures/Story3.png">
  </p>

Il est également possible de mesurer l’aire d’un bâtiment, et de visualiser les coordonnées, la hauteur et la pente d’un point à la volée.
  

<p align="center">
<img src="/Figures/Story4.png"> <img src="/Figures/Story5.png">
  </p>
  
  
  
  
  
  
  
  
</div>

