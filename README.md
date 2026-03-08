# README - TP01 - Gestionnaire de produits

> **Cours :** 420-W40-SF - Développement d’applications Web (Cégep de Sainte-Foy)
> **Travail :** TP01 - Gestionnaire de produits
> **Étudiant(e) :** Gabriel Roy
> **Repo GitHub :** "https://github.com/GabrielRoy/appweb-trpr01"
> **Déploiement (GitHub Pages) :** {{ 'https://gabrielroy.github.io/appweb-trpr01/' }}

---

**IMPORTANT**: renommer README.md

## 1) Description du projet

Décrire en 5–10 lignes l’application réalisée :

- Contexte :
  Le site a été créé pour les gérant de l'inventaire d'un magasin de jeux vidéo. Il facilite la gestion de l'inventaire en permettant de voir clairement ce qu'il y a à l'intérieur de celui-ci. On peut y retrouver les informations importantes du produit comme le nom, la description, l'id, le prix et surtout le nombre restant dans l'inventaire.
- Objectif principal :
  Faciliter la gestion de l'inventaire et voir en avance ce qu'il y a à l'intérieur.
- Public cible / usage typique :
  Les gestionnaires de l'inventaire du magasin. Il permet de voir le nombre de stock restant facilement, de modifier facilement le contenu de l'inventaire et d'ajouter des produits à celui-ci.

**Produit choisi :** Système de gestion d'un inventaire d'un magasin de jeux vidéo

---

## 2) Fonctionnalités (récits utilisateurs)

- [x] Ajouter un formulaire d'ajout d'un jeu vidéo en entrant les informations.
- [x] Ajouter un formulaire de modification d'un jeu vidéo en entrant les informations.
- [x] Afficher la liste des produits dans l'inventaire.
- [x] Afficher les informations des produits dans l'inventaire.
- [x] Afficher les informations du produit qui vient d'être selectionné par l'utilisateur.
- [x] Avoir la possibilité de dupliquer un produit.
- [x] Avoir la possibilité de supprimer un produit de l'inventaire.
- [x] Avoir un affichage clair et visible des produits pour savoir si le stock de celui-ci est bas.
- [x] Avoir un message d'erreur lorsque le stock d'un produit devient très bas.
- [x] Pouvoir trier l'inventaire à l'aide d'un champ de recherche.
- [x] Pouvoir exporter le contenu de l'inventaire en .csv.
- [x] Mettre sur github page.

> Ajouter ici toute fonctionnalité optionnelle (ex. catégorie, actif, date de création, etc.).

---

## 3) Technologies utilisées

- Node.js
- Vue
- Bootstrap

---

## 4) Installation et démarrage

### Prérequis

- Node.js LTS

### Installation

```bash
npm install
```

### Démarrage en dev

```bash
npm run dev
```

### Build

```bash
npm run build
```

---

## 5) Déploiement (GitHub Pages)

- **Nom du repo / dossier GitHub Pages :** `appweb-trpr01`
- **URL attendue :** {{ `https://gabrielroy.github.io/appweb-trpr01/` }}

### Notes de configuration

- base URL (`base`) de Vite ajustée pour GitHub Pages
- commandes utilisées pour déployer (si script)

---

## 6) Architecture et organisation du code

Décrire la structure du projet et les responsabilités.

### Structure des dossiers

- `src/components/` : composants UI (responsabilité unique)
- `src/models/` : types/interfaces TypeScript (ex. `Product`)
- `src/scripts/` : script du système.
- `src/css/` : fichier css du système

> Adapter à votre projet réel. L’objectif est d’expliquer **où** se trouve la logique et **pourquoi**.

### Composants clés

- `AddProductFormComponent` : C'est le formulaire d'ajout d'un produit. Il a comme tâche de prendre en note les informations données et de les vérifier avant de les envoyer au parent qui s'occupe de stocker le nouveau produit.
- `MainPageComponent` : C'est la base du site. Il détient tous les composant et affiches ceux qui sont nécessaire. Il contient aussi la "DB" pour stocker les produits créés.
- `ProductListComponent` : C'est l'encadrée autour des produit (le tableau). Il s'occupe de contenir et d'afficher les produits présent dans le stockages et un message de stockage vide si besoin. Il s'occupe aussi de filtrer les produits afficher avec l'aide de SearchQueryComponent.
- `ProductListItemComponent` : Il s'occupe d'afficher les informations de son produit et de faire d'envoyer ce qui est nécessaire aux parents si une action est demandé par l'utilisateur (delete, update, dupliquer)
- `SearchQueryComponent` : Il s'occupe de prendre en input le string du nom demandé et l'envoie au parent que lui va trier la liste avec.
- `ShowProductComponent`: Il s'occupe d'afficher les informations, en format plus détaillé, d'un produit que l'utilisateur a sélectionné dans la liste.
- `UpdateProductFormComponent` : Il s'occupe, en tant que formulaire, de modifier les informations du produit qu'il a reçu en paramètre.

---

## 7) Utilisation de l’IA (OBLIGATOIRE)

> **IMPORTANT :** Toute omission d’utilisation d’IA (même pour UI/CSS) peut entraîner **0** et une mention de plagiat.

### Outil(s) utilisé(s)

- _Nom des outils (ex. ChatGPT, Copilot, etc.)_
- ChatGPT et copilot

### Comment l’IA a été utilisée

Décrire concrètement :

- Aide au débug
- Création de méthode
- css (visuel du site)

### À quel endroit

\_Où le CSS normal et de bootstrap est présent donc tous les fichiers de components.

Dans certain fichier avec des méthodes.\_\_

#### MainPageComponent

- Ligne 128 à 136. Pour pouvoir envoyer les informations du produit à dupliquer au formulaire d'ajout pour qu'il se remplisse.
- Ligne 66 à 96 : Pour coder la fonction qui permet d'obtenir l'inventaire sous forme de fichier excel.

#### UpdateProductFormComponent

- Ligne 21 à 44: Pour gérer les informations du formulaire et créer les erreurs au besoin.

#### AddProductFormComponent

- Ligne 19 à 49: Pour gérer les informations du formulaire et créer les erreurs au besoin.
- Ligne 54 à 59: Pour gérer le préremplissage des champs lors de la dupplication.

#### ProductListComponent

- Ligne 37 à 45: Pour gérer l'affichage des warnings des stock faibles.

#### SearchQueryComponent

- Entièreté du fichier fait avec l'intellisence de VSCODE qui a aidé dès qu'il a vue ce que je voulais faire.

### Exemples de prompts (2 à 5)

1. “Peux tu me dire comment faire la gestion d'erreur avec ces champs : {Nom, description, stock, prix}”
2. “Comment fait t'on pour remplir un formulaire avec les informations provenant d'un parent.”
3. "Comment créons-nous un fichier .csv"
