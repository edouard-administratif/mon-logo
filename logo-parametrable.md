# Logo paramétrable — règles et suivi

Ce document accompagne [`logo-parametrable.html`](logo-parametrable.html). Il décrit les choix actuellement appliqués. À chaque itération du logo ou de la page, mettre à jour les règles concernées et ajouter une entrée au suivi ci-dessous.

## Source et interprétation des formes

Le dessin de départ est [`logo-fusionné.svg`](../OneDrive/Documents/_Documents/logo-fusionné.svg). La page HTML en reprend la disposition générale, mais reconstruit les bandeaux pour appliquer l'épaisseur commune. Les noms attribués aux éléments sont les suivants :

| Partie | Forme dans le SVG | Règle actuelle |
| --- | --- | --- |
| Cheveux | Deux bandeaux diagonaux réunis en un contour | Même épaisseur normale `e` ; trois paramètres propres aux cheveux : inclinaison, hauteur totale et position de la raie. |
| Yeux | Deux cercles ou deux bandeaux horizontaux | Une case à cocher choisit le mode. En mode bandeaux, leur épaisseur normale vaut `e` et leur taille est leur longueur. |
| Oreilles | Deux bandeaux verticaux | Même épaisseur et même longueur ; leur bord supérieur reste fixe ; leur longueur règle le départ des joues. |
| Barbe des joues | Deux bandeaux diagonaux | Même épaisseur normale ; chaque joue finit sur le bord visible du menton. |
| Barbe du menton | Deux bandeaux horizontaux superposés | Le second repose sur le premier ; chacun a l'épaisseur commune. Après calcul, leur union avec les joues est dessinée par un seul contour. |

**Interprétation actuelle de « posé sur » :** les deux bandeaux horizontaux du menton se touchent bord à bord, l'un au-dessus de l'autre.

## Paramètres de la page

| Réglage | Valeur initiale | Plage / comportement |
| --- | --- | --- |
| Couleur des cheveux | Noir `#000000` | Sélecteur de couleur. |
| Couleur des yeux | Noir `#000000` | Sélecteur de couleur commun aux deux yeux. |
| Couleur des oreilles | Noir `#000000` | Sélecteur de couleur commun aux deux oreilles. |
| Couleur de la barbe | Noir `#000000` | Sélecteur de couleur. |
| Fond de l'aperçu | Blanc `#ffffff` | Modifie seulement l'aperçu, pas le SVG exporté. |
| Épaisseur commune des bandeaux `e` | 8 unités SVG | De 5 à 12 ; s'applique à tous les bandeaux, y compris aux yeux quand le mode bandeaux est activé. |
| Taille des yeux en mode disques | 13,5 unités SVG | Diamètre de chacun des deux disques ; de 8 à 20,3 unités SVG. |
| Yeux en bandeaux horizontaux | Désactivé | Remplace les cercles par deux bandeaux horizontaux d'épaisseur `e`. |
| Taille des yeux en mode bandeaux | 13,5 unités SVG | De 5 à 25 ; devient la longueur de chacun des deux bandeaux. La dernière valeur de chaque mode est conservée quand on bascule. |
| Écart des yeux | 0 | Déplacement symétrique de −5 à +5 unités SVG. |
| Hauteur des cheveux | 13,4 unités SVG | De −20 à 60 ; distance verticale entre le point le plus bas des cheveux et le centre des yeux. L'augmenter remonte seulement les cheveux. |
| Hauteur des yeux | 16,2 unités SVG | De −20 à 60 ; distance verticale entre le centre des yeux et le point le plus haut de la barbe, au départ des joues sous les oreilles. L'augmenter remonte ensemble les yeux et les cheveux. |
| Longueur des oreilles | 14,5 unités SVG | De 8,7 à 21,8 ; hauteur de chacun des deux bandeaux verticaux. |
| Longueur des joues | 9,4 unités SVG | De 2,1 à 22 ; distance verticale du haut de la barbe au haut du menton. L'augmenter abaisse le menton ; les oreilles restent fixes. |
| Inclinaison des cheveux | 0° | De −15° à +15°, par pas de 0,1°. À 0°, les deux extrémités basses sont à la même hauteur. L'angle règle la pente de la ligne qui les relie. |
| Épaisseur des cheveux | 15,4 unités SVG | De `e` à 25 ; distance verticale entre le point le plus haut et le point le plus bas des cheveux lorsque l'inclinaison vaut 0°. La borne minimale suit donc l'épaisseur normale commune des bandeaux. |
| Position de la raie | 0,48 | De −1 (tout à gauche) à +1 (tout à droite), avec 0 exactement au centre. Aux extrêmes, un seul des deux bandeaux diagonaux subsiste. |

Le libellé du curseur reste **« Taille des yeux »** dans les deux modes ; seule la signification de sa valeur change. La page affiche des nombres sans unité ; seule l'inclinaison porte le symbole `°`. Les longueurs sont calculées dans les coordonnées du SVG et la raie utilise l'échelle de −1 à +1.

Les longueurs sont affichées **au dixième** et leurs valeurs initiales sont elles aussi arrondies au dixième. Les calculs géométriques conservent leur précision ; le dessin initial peut différer très légèrement de la version précédente. La raie reste affichée au centième.

Le bouton **Réinitialiser** remet tous les réglages à leurs valeurs initiales. Le bouton **Télécharger le SVG** exporte le dessin avec les réglages visibles. Le fond de l'aperçu n'est pas inclus : le fichier exporté a un fond transparent.

## Règles de modification

1. **Invariant prioritaire : tous les bandeaux ont une épaisseur commune `e`.** Pour chaque portion rectiligne, `e` est la distance entre ses deux bords parallèles mesurée sur la normale à la direction principale de cette portion. Ce n'est ni sa largeur suivant `x`, ni sa hauteur suivant `y` : pour un bandeau oblique, ces projections sont différentes de `e`.
2. Une variation de longueur, d'angle ou de forme doit conserver cette même valeur `e` pour **tous** les bandeaux. Une éventuelle commande d'épaisseur devra modifier `e` globalement, jamais l'épaisseur d'un seul bandeau. Un étirement non uniforme d'un tracé oblique ne respecte pas cette règle.
3. **Tous les bandeaux diagonaux ont leurs deux bouts coupés verticalement.** À chaque bout, les bords supérieur et inférieur ont la même abscisse. Pour une pente `m`, leur écart vertical vaut `e × √(1 + m²)` ; l'épaisseur mesurée sur la normale vaut donc bien `e`.
4. Le **coin inférieur intérieur de chaque oreille** touche exactement le **coin supérieur extérieur du bandeau de joue** correspondant. Côté gauche : coin inférieur droit de l'oreille et coin supérieur gauche de la joue ; côté droit : coin inférieur gauche de l'oreille et coin supérieur droit de la joue.
5. Le **bas du menton et celui des joues forment une ligne continue au raccord visible**. La joue gauche se termine exactement au bord gauche du menton, la droite au bord droit ; leurs coins inférieurs ont la même ordonnée que le bord inférieur du menton. Aucun prolongement de joue caché sous le menton ne doit servir à satisfaire cette règle.
6. Après calcul des deux joues et des deux bandeaux horizontaux du menton, dessiner leur **union comme un seul tracé**, sans trait intérieur ni filet blanc. Supprimer les points inutiles du contour.
7. Pour les cheveux à **0°**, le bas extérieur du bandeau gauche et celui du bandeau droit sont alignés horizontalement. Leur écart vertical du haut à la raie définit l'« épaisseur des cheveux » demandée ici, sans modifier `e`.
8. La raie se déplace linéairement entre les deux extrémités des cheveux : −1 à gauche, 0 au milieu, +1 à droite.
9. Au raccord des deux bandeaux de cheveux, prolonger ou couper leurs **bords inférieurs jusqu'à leur intersection**. Leur contour fusionné n'a pas de segment vertical intérieur ni d'encoche à la raie.
   À la valeur minimale de hauteur (`hauteur = e`), les cheveux forment un seul bandeau plat à 0° ; la raie n'est alors pas visible. Si `e` augmente au-delà de la hauteur choisie, remonter automatiquement celle-ci à `e`.
10. Mesurer les deux hauteurs **verticalement depuis le centre commun des yeux** : centre des yeux → bas des cheveux, puis centre des yeux → **haut de la barbe** (le plus haut des deux départs des joues).
11. **Les deux commandes de hauteur ne modifient jamais la barbe, ses raccords ni l'inclinaison des joues.** La barbe est l'ancre verticale. Augmenter « Hauteur des yeux » remonte les yeux et les cheveux ensemble. Augmenter « Hauteur des cheveux » remonte les cheveux seuls. Cocher le mode bandeaux ou changer la taille des yeux conserve ces deux valeurs, le centre des yeux et la position des cheveux.
12. La commande de longueur des joues déplace le menton vers le bas ; les oreilles et le haut des joues restent fixes.
13. Préserver la disposition générale de `logo-fusionné.svg` aux valeurs initiales, sous réserve des corrections nécessaires pour les règles géométriques ci-dessus.
14. Garder les parties identifiables dans le modèle, même si plusieurs bandeaux sont fusionnés pour le dessin final.
15. Appliquer les réglages des yeux et des oreilles de façon symétrique tant qu'aucune asymétrie n'est demandée.
   En mode yeux en bandeaux, utiliser la même épaisseur `e` que les autres bandeaux, et mesurer les deux écarts verticaux depuis les bords de ces bandeaux.
16. Garder la page autonome : elle doit fonctionner comme fichier HTML local, sans bibliothèque ni connexion réseau.
17. Synchroniser ce document avec les contrôles et le comportement réellement présents dans la page.

La géométrie des bandeaux diagonaux est recalculée à chaque modification ; la page n'utilise plus d'étirement vertical de la barbe.

## Suivi des itérations

### 2026-11-10 — Première page

- Reprise de la géométrie de `logo-fusionné.svg` dans un SVG intégré à `logo-parametrable.html`.
- Création des réglages de couleur et de forme décrits ci-dessus.
- Ajout de la réinitialisation et de l'export SVG.

### 2026-11-11 — Documentation

- Création de ce fichier pour conserver les règles et les décisions au fil des prochaines itérations.
- Ajout de l'invariant d'épaisseur commune des bandeaux, mesurée perpendiculairement à leur direction, et identification du réglage de barbe actuel à corriger.
- Précision : l'invariant concerne tous les bandeaux, même obliques, et une future variation d'épaisseur devra être globale.
- Identification des cheveux, des joues et du menton comme bandeaux distincts, en plus des oreilles ; les yeux étaient alors uniquement des cercles, avant l'ajout du mode bandeaux.
- Ajout de l'épaisseur globale `e` dans la page, reconstruction géométrique des diagonales avec coupes verticales et remplacement de l'étirement de la barbe.
- Calcul de la barbe comme contour unique : disparition de la jonction entre les bandeaux du menton et simplification des sommets alignés.
- Liaison exacte entre le coin inférieur intérieur de chaque oreille et le coin supérieur extérieur de la joue correspondante.
- Alignement du bas du menton avec le bas des joues à leurs extrémités intérieures.
- Correction du raccord visible : les joues finissent maintenant aux bords du menton, avec leurs coins inférieurs exactement au niveau du bas du menton.
- Ajout des trois paramètres des cheveux : inclinaison référencée à deux bas alignés à 0°, hauteur totale à 0° et position de la raie de −1 à +1. Les deux parties sont dessinées dans un seul contour.
- Ajout des deux distances verticales entre cheveux, yeux et menton. Le réglage de longueur de barbe est renommé « longueur des joues » et agit sur le départ des joues, afin que la distance yeux–menton reste indépendante.
- Adaptation automatique du cadrage SVG aux grands écarts et de la position verticale des oreilles quand le menton remonte.
- Correction du raccord des cheveux : les deux bords inférieurs se rencontrent à leur intersection calculée, ce qui élimine l'encoche. La hauteur minimale des cheveux passe à 13,5 pour garder ce raccord dans le contour sur toute la plage des réglages.
- Ancrage vertical du menton : les deux distances déplacent les yeux et/ou les cheveux vers le haut, sans recalculer la barbe ni l'inclinaison des joues.
- La hauteur minimale des cheveux suit désormais l'épaisseur commune `e`. Au minimum, le raccord disparaît dans un bandeau unique ; les valeurs juste au-dessus restent sans encoche et conservent la hauteur demandée.
- Correction de la référence du deuxième écart : il va du bas des yeux au **haut de la barbe** au départ des joues, et non au haut du menton. Sa valeur initiale devient 9,4 pour conserver presque la même disposition par défaut.

- Correction du sens de la longueur des joues : l’allonger abaisse le menton sans remonter les oreilles. Le second écart reste référencé au haut de la barbe.
- Ajout du mode « yeux en bandeaux horizontaux » : la taille des yeux devient leur longueur, leur hauteur vaut `e`, et les distances verticales restent mesurées entre bords visibles.
- Le libellé « Taille des yeux » reste identique entre les modes disques et bandeaux.
- Le changement de mode des yeux ajuste automatiquement « Hauteur des cheveux » et « Hauteur des yeux » pour garder les positions relatives des cheveux, du centre des yeux et de la barbe.
- En mode disques, une modification de « Taille des yeux » ajuste les mêmes hauteurs pour préserver ces positions.
- Les deux hauteurs sont désormais mesurées depuis le centre des yeux. Valeurs initiales : 13,4 pour les cheveux et 16,2 pour les yeux. Changer la forme ou la taille des yeux ne modifie plus ces valeurs.
- Les derniers pourcentages ont été remplacés par des unités SVG pour le diamètre des yeux en mode disques, la hauteur des oreilles et la longueur des joues ; les valeurs initiales conservent la géométrie précédente.

- Suppression des unités affichées à côté des curseurs ; seul le symbole des degrés reste visible.
- Arrondi de l'affichage des longueurs au dixième, sans arrondir la géométrie interne du logo.
- Arrondi des valeurs initiales elles-mêmes au dixième : diamètre des yeux 13,5, longueur des oreilles 14,5 et longueur des joues 9,4.
- Valeurs initiales ajustées : écart cheveux–yeux 6,6 et inclinaison des cheveux 0°.
- Libellés abrégés en « Hauteur des cheveux » et « Hauteur des yeux », sans changer la mesure entre bords ni le mouvement associé.
- Libellé « Épaisseur des cheveux (hauteur à 0°) » abrégé en « Épaisseur des cheveux » ; sa définition géométrique reste inchangée.
