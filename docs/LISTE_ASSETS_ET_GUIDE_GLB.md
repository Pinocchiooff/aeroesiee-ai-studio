# Guide des assets et des modèles GLB — Simulateur AéroESIEE

Tous les assets proposés ci-dessous sont annoncés CC0 par leurs sources, mais vérifiez la licence sur la page de chaque asset avant de l’utiliser. Téléchargez les fichiers une seule fois et stockez-les dans le projet plutôt que d’appeler les API des catalogues en production.

## Textures

Choisissez de préférence une résolution 1K (2K pour le sol principal). Les cartes usuelles sont `diff` (albedo/couleur), `nor_gl` (normal OpenGL, convenant à Three.js), `rough` (rugosité) et `ao` (occlusion, si fournie). `disp` est facultative.

| Usage | Asset proposé | Source | Dossier sous `public/assets/` |
|---|---|---|---|
| Sol principal herbe/roche | `aerial_grass_rock` | Poly Haven | `textures/grass_rock/` |
| Sol forestier | `forest_ground_04` | Poly Haven | `textures/forest_ground/` |
| Terre et feuilles | `brown_mud_leaves_01` | Poly Haven | `textures/dirt_leaves/` |
| Terre nue | `brown_mud_02` | Poly Haven | `textures/mud/` |
| Rivage rocheux | `coast_sand_rocks_02` | Poly Haven | `textures/coast_rocks/` |
| Sable | `coast_sand_04` ou `sand_03` | Poly Haven | `textures/sand/` |
| Galets | `sand_rocks_small_01` | Poly Haven | `textures/shore_pebbles/` |
| Falaises | `cliff_side` | Poly Haven | `textures/cliff/` |
| Roche | `rock_wall_04`, `rock_08` ou `aerial_rocks_04` | Poly Haven | `textures/rock/` |
| Roche alternative | `Rock030` ou `Rocks007` | ambientCG | `textures/rock_alt/` |
| Enduit/brique | `rough_plasterbrick_05` | Poly Haven | `textures/plaster/` |
| Asphalte, béton, bardage métallique | Chercher « asphalt », « concrete », « corrugated metal » | Poly Haven / ambientCG | `textures/asphalt/`, `textures/concrete/`, `textures/metal_cladding/` |
| Eau | Texture choisie ou eau générée en code | ambientCG ou code | `textures/water/` |

Une sélection d’environ 10 à 14 textures suffit pour un premier rendu.

## Modèles 3D

| Usage | Asset/recherche | Destination sous `public/assets/` |
|---|---|---|
| Rocher | `rock_boulder_dry` (Poly Haven) | `models/rocks/rock_boulder_dry.glb` |
| Arbres | « tree », « pine », « birch », « oak » | `models/trees/` |
| Plantes | « bush », « fern », « grass clump » | `models/plants/` |
| Bâtiments | « hangar », « control tower », « warehouse », « building » | `models/buildings/` |
| Quadricoptère | « quadcopter », « drone » | `models/vehicles/quad.glb` |
| Avion | « airplane », « RC plane », « cessna » | `models/vehicles/fixedwing.glb` |

Sources possibles : Poly Haven, 3DAssets.dev, Quaternius et Sketchfab. Vérifiez la licence de chaque fichier et notez son nom, son auteur et son URL. Ne supposez pas qu’un résultat de recherche est CC0 sans vérifier sa page de licence.

## Préparer et optimiser les GLB

- Le GLB peut embarquer géométrie et textures ; glTF peut aussi être distribué en plusieurs fichiers (`.gltf`, `.bin` et textures).
- Vérifiez le modèle dans un visualiseur glTF : textures, pièces manquantes, échelle et complexité. Visez moins de 30 000 triangles pour un arbre LOD0 et moins de 200 000 pour un drone.
- Nommez les fichiers sans espaces ni accents, par exemple `pine_01.glb`, `pine_01_lod1.glb`.
- Conventions recommandées : mètres, axe Y vers le haut, avant vers -Z ; origine d’un arbre au pied du tronc ; supprimer caméras et lumières inutiles.
- Pour convertir et optimiser avec glTF Transform, installez l’outil localement et consultez `gltf-transform --help`, car les options peuvent dépendre de la version :

```sh
npm install -g @gltf-transform/cli
gltf-transform copy modele.gltf modele.glb
gltf-transform optimize modele.glb modele_opt.glb --compress meshopt --texture-compress webp
gltf-transform resize modele_opt.glb modele_1k.glb --width 1024 --height 1024
gltf-transform simplify modele_opt.glb modele_lod1.glb --ratio 0.3
```

### Pièces mobiles des drones

Pour commencer, une approche hybride est pratique : utiliser le GLB pour le fuselage/bras et garder hélices et gouvernes procédurales, avec des points d’ancrage définis dans le code. Sinon, séparez les pièces mobiles et donnez-leur des noms stables.

- Quadricoptère : `rotor_0` à `rotor_3`, avec sens de rotation documenté, et `fpv_mount`.
- Aile fixe : `prop`, `aileron_L`, `aileron_R`, `elevator`, `rudder`, `fpv_mount`.

Dans Blender, placez l’origine de chaque pièce sur son axe de rotation. Exportez en glTF Binary (`.glb`), +Y up, après application des transformations.

## Manifeste et crédits

Le manifeste central est `public/assets/manifest.json`. Gardez les chemins relatifs à `public/assets/`, adaptez les noms des cartes aux noms réellement téléchargés et n’ajoutez au manifeste que les fichiers présents. Consignez pour chaque asset son auteur, sa licence et son URL. Le manifeste ne remplace pas la vérification des licences.
