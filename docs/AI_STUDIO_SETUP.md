# Préparer les ressources pour Google AI Studio

Ce dépôt organise les ressources du Simulateur AéroESIEE. Il ne contient pas encore le code de l’application ni les fichiers ZIP/GLB/textures annoncés ; le manifeste reste donc volontairement vide jusqu’à l’ajout et la vérification des assets réels.

## Consignes pour l’intégration

1. Traiter `public/assets/manifest.json` comme source de vérité pour les chemins, catégories et crédits.
2. Charger les ressources statiques depuis `/assets/...` dans une application web servie avec la convention `public/`. Les chemins du JSON sont relatifs à `public/assets/`; préfixer par `/assets/` au moment de construire l’URL.
3. Pour Three.js, utiliser `GLTFLoader` pour les GLB et `TextureLoader` (ou `LoadingManager`) pour les cartes de texture. Pour une texture PBR, associer `albedo` à `map`, `normal` à `normalMap`, et `roughness` à `roughnessMap` selon les matériaux utilisés. Respecter l’espace colorimétrique sRGB pour l’albedo et les espaces linéaires appropriés pour les données non colorimétriques.
4. Vérifier qu’un fichier référencé existe avant son chargement et afficher une erreur compréhensible si un asset manque ; prévoir des matériaux/modèles de remplacement afin que la scène reste utilisable.
5. Ne pas inventer d’URL, de fichiers, d’auteurs ou de licences. N’utiliser que les entrées réellement présentes dans le manifeste et conserver les crédits.
6. Éviter de charger les fichiers depuis les API des bibliothèques d’assets en production. Un dépôt privé n’est pas une URL publique d’assets ; utiliser l’import/synchronisation du projet ou un hébergement autorisé avec CORS, sans publier un dépôt privé.
7. Conserver les pièces mobiles de drone compatibles avec les rigs existants. Si un modèle n’offre pas de nœuds mobiles, garder les hélices/gouvernes procédurales et utiliser le modèle uniquement pour le corps.

## Prompt à copier dans AI Studio

> Examine le dépôt et utilise `docs/AI_STUDIO_SETUP.md`, `docs/LISTE_ASSETS_ET_GUIDE_GLB.md` et `public/assets/manifest.json` comme documentation. N’invente aucun asset : le manifeste est la source de vérité. Les fichiers de `public/assets/` sont servis sous `/assets/`; les chemins du manifeste sont relatifs à `public/assets/`. Intègre les textures et modèles présents en utilisant les chargeurs adaptés (Three.js si le projet utilise Three.js), gère les erreurs et prévois des remplacements visuels si une ressource manque. Préserve les rigs et les pièces mobiles des drones. Respecte les licences et crédits. Avant de modifier le code, indique les ressources effectivement trouvées et les chemins utilisés.

## Contrôles à effectuer après ajout des archives

- Inventorier les fichiers extraits et détecter les doublons exacts par SHA-256 ; examiner aussi les noms/contenus proches avant de supprimer quoi que ce soit.
- Vérifier les formats, dimensions des textures, poids et présence des GLB.
- Contrôler que chaque chemin du manifeste correspond à un fichier et que le JSON est valide.
- Tester le chargement dans l’application et vérifier les erreurs réseau/CORS.
- Vérifier les licences et compléter les crédits avant publication.
