# Comparatif : Mapbox vs Overpass pour Carto Laser

## 1. L'API Mapbox
**Coût** : Gratuit (jusqu'à 50k chargements/mois), donc négligeable pour un petit groupe.
**Architecture** : Basé sur des "Tuiles Vectorielles" (Carrés pré-découpés).

### Avantages
- **Esthétique** : Données très propres, lissées, belles couleurs par défaut.
- **Support Web** : Très performant pour l'affichage écran.

### Inconvénients majeurs (Critique pour Laser)
- **Découpage en Tuiles (Le "Piege")** : Mapbox découpe la terre en une grille de carrés (Tuiles). Une rivière qui traverse la carte est techniquement coupée en plusieurs segments à chaque bordure de tuile.
    - **Conséquence Laser** : La découpeuse laser va s'arrêter et reprendre à chaque ligne de tuile, créant des points de brûlure ou des discontinuités. Recoudre ces morceaux ("Stitching") est mathématiquement très complexe et sujet aux bugs.
- **Accès Donnée** : Extraire un SVG "propre" depuis Mapbox GL JS est difficile car le rendu se fait dans un Canvas (image bitmap). Il faut des outils tiers lourds.

## 2. Solution Actuelle (Leaflet + Overpass)
**Architecture** : Chargement de donnée brute (XML/JSON OSM) sur une zone rectangulaire définie.

### Avantages
- **Seamless (Sans coupure)** : On télécharge l'objet "Rivière" entier d'un seul bloc. Pas de lignes de coupe artificielles.
- **Contrôle Total** : On décide nous-même de l'épaisseur exactes et de transformer les traits en formes (via l'algorithme V12 ajouté ce jour).
- **Format Vectoriel** : On génère le SVG maths par maths, garantissant une précision absolue pour la machine.

## Conclusion
*   Pour une **Gallerie Web** ou un **GPS** : Mapbox gagne haut la main.
*   Pour un **Outil de Manufacturing (Laser / CNC)** : L'approche Overpass (Raw Data) est techniquement supérieure car elle évite le problème de la mosaïque de tuiles.

*Note : La mise à jour V12 (déployée ce jour) intègre `Turf.js` pour fusionner toutes les rivières en une seule forme, simulant ce que Mapbox fait visuellement, mais en gardant la précision manufacturière.*
