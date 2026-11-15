# Simulateur AéroESIEE — ressources pour Google AI Studio

Dépôt privé de documentation et d’assets du simulateur AéroESIEE.

## Organisation

- [`docs/LISTE_ASSETS_ET_GUIDE_GLB.md`](docs/LISTE_ASSETS_ET_GUIDE_GLB.md) : catalogue des assets souhaités et guide de préparation des modèles GLB.
- [`docs/AI_STUDIO_SETUP.md`](docs/AI_STUDIO_SETUP.md) : consignes à transmettre à AI Studio pour intégrer les ressources.
- [`public/assets/manifest.json`](public/assets/manifest.json) : manifeste central des textures, modèles et crédits.
- `public/assets/textures/<catégorie>/` : cartes PBR.
- `public/assets/models/<catégorie>/` : modèles GLB.

## État des fichiers et doublons

Au dernier contrôle, le dépôt ne contenait que ce README. Aucun ZIP ni autre document nouvellement chargé n’était visible dans le dépôt ou accessible comme pièce jointe exploitable. Le guide partagé dans la conversation a été classé sous `docs/`. Aucun fichier binaire n’a été extrait, renommé ou supprimé ; aucun doublon ne peut donc être confirmé pour les archives absentes.

Quand les archives seront ajoutées au dépôt ou jointes ici de façon accessible, il faudra les inventorier, comparer leurs contenus (noms et empreintes), conserver une seule copie de chaque asset et mettre à jour le manifeste à partir des fichiers réellement présents.

## Chargement dans l’application

Dans un projet web utilisant le dossier `public`, chargez les ressources par des URL comme `/assets/models/rocks/rock_boulder_dry.glb`. Les chemins enregistrés dans le manifeste sont relatifs à `public/assets/`. Le manifeste est un inventaire de ressources, pas un chargeur automatique : le code de l’application doit le lire et créer les matériaux/modèles.

Un dépôt GitHub privé n’est pas automatiquement accessible depuis AI Studio ou depuis une application déployée. Importez/synchronisez les assets dans le projet ou utilisez l’hébergement autorisé par l’application. Ne rendez pas le dépôt public pour contourner les permissions ; évitez d’exposer des URL publiques pour des fichiers soumis à des restrictions.

## À faire lorsque les ZIP seront disponibles

1. Décompresser et examiner les archives sans écraser les fichiers existants.
2. Détecter les doublons exacts par empreinte, puis les doublons probables par nom et contenu.
3. Conserver les fichiers utiles dans `public/assets/`, avec noms cohérents et sans accents.
4. Vérifier les licences et ajouter les crédits dans `public/assets/manifest.json`.
5. Tester le JSON et vérifier que chaque chemin du manifeste correspond à un fichier présent.
