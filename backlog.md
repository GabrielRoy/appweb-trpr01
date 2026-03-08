# Backlog - TP01 - Gestionnaire de produits

> **Cours :** 420-W40-SF - Développement d’applications Web (Cégep de Sainte-Foy)
> **Travail :** TP01 - Gestionnaire de produits
> **Étudiant(e) :** {{ Gabriel Roy }}
> **Dernière mise à jour :** {{ 2026-02-20 }}

---

## 1) Règles de backlog (à respecter)

- **Tâches petites** : idéalement 25 à 50 minutes.
- **Titres explicites** : “UI liste produits (tableau)” au lieu de “liste”.
- **Critères d’acceptation** : 1 à 3 points simples pour savoir si c’est “done”.
- **Ordre logique** : setup → affichage → interactions → validations → export → déploiement → finitions.
- **Suivi** : on bouge les statuts au fur et à mesure (visible).
- **Légende statut :** ⬜ À faire | 🟦 En cours | ✅ Fait | 🟥 Bloqué
- Priorités
  - **MUST** : requis par l’énoncé (récits 1 à 10 + méthodologie)
  - **SHOULD** : qualité/robustesse (cas limites, petits refactors)
  - **COULD** : bonus / nice-to-have (si tout le reste est stable)
- **IMPORTANT**: renommer backlog.md

---

## 2) Tableau du backlog

> Copiez/collez des lignes au besoin.

| ID  | Priorité | Statut | Titre (tâche)                                                                                             |          Relié à (RU#)           | Critères d’acceptation (définition de done)                                                                       | Notes / obstacles                                                                             |
| :-- | :------- | :----: | :-------------------------------------------------------------------------------------------------------- | :------------------------------: | ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
|     |          |        |                                                                                                           |                                  |                                                                                                                   |                                                                                               |
| A1  | MUST     |   ✅   | Finir MainPage.vue                                                                                        |          Base d'un site          | La page et tous les composants affichent et fonctionnent.                                                         | Lier les composants ensembles et faire le css                                                 |
| B1  | MUST     |   ✅   | Faire et implémenter le formulaire de création pour que les produits s'ajoutent.                          |                1                 | Le formulaire affiche et fonctionne pour la modification et création.                                             | Envoyer correctement le produit à la liste pour que le produit affiche.                       |
| B2  | MUST     |   ✅   | Faire l'affichage du produit un fois cliqué.                                                              |                7                 | Une fois cliqué, le produit et ses informations sont affichés.                                                    | Envoyer le produit selectionné au composant qui l'affiche.                                    |
| C1  | MUST     |   ✅   | Pouvoir supprimer un produit.                                                                             |                4                 | Une fois le boutton cliqué, la liste des produits dans le stockage est modifier pour supprimer le produit.        | Filtrer correctement la liste du stockage pour qu'elle 'supprime' le produit.                 |
| C2  | MUST     |   ✅   | Afficher les produits                                                                                     |                5                 | Une liste est présente et elle a tous les produits présent dans le stockage                                       | Lier la liste des produits avec le stockage.                                                  |
| C3  | MUST     |   ✅   | Affichage en temps réel des quantités avec indicateur visuel                                              |                8                 | Les quantités se mettent à jour immédiatement et les couleurs changent selon la quantité (ex: vert, jaune, rouge) | Faire que la quantité sois visiblemment représenter. (21+ vert, 11+ jaune, reste rouge)       |
| C4  | MUST     |   ✅   | Notification lorsqu'un produit atteint un stock critique                                                  |                9                 | Un message apparaît sous la liste indiquant tous les produits en stock critique                                   | Afficher correctement le produit et son nom pour faciliter la compréhension de l'utilisateur. |
| C5  | MUST     |   ✅   | Bouton "Dupliquer" qui préremplit un nouveau formulaire avec les données du produit sélectionné           |                3                 | Le formulaire de création se remplit avec les données du produit.                                                 | Envoyer les données du produit au formulaire de création.                                     |
| D1  | MUST     |   ✅   | Faire et implémenter le formulaire de modication du produit.                                              |                2                 | Le formulaire permet de modifier un produit sans en créer un nouveau.                                             | Confirmer qu'un nouveua produit n'est pas créer mais seulement modifier.                      |
| D2  | MUST     |   ✅   | Faire que le formulaire de modication se préremplisse.                                                    |                2                 | Le formulaire se préremplis avec les informations nécessaires.                                                    | Correctment envoyer le produit et préremplir les chmaps.                                      |
| D3  | MUST     |   ✅   | Les données sont vérifier avant d'être changé ou ajouté. Un message d'erreur apparait où il y a problème. |             1,2 et 3             | Un message d'erreur apparait en cas de mauvaise donnée.                                                           | Difficulter à facilement montrer à l'utilisateur qu'elle donnée est invalide.                 |
| D4  | MUST     |   ✅   | Avant de suprimer un produit une demande de confirmation est faite à l'utilisateur.                       |                4                 | Le message de confirmation est affiché une fois cliquer sur le boutton.                                           | Afficher la demande de confirmation à la bonne place. (Sur le produit)                        |
| D5  | MUST     |   ✅   | Avoir la possibilité d'exporter en fichier .csv les produits dans le stockage.                            |                10                | Un fichier .csv est créer et à l'intérieur les informations des produits sont présent.                            | Comprendre comment exporter en .csv                                                           |
| D6  | MUST     |   ✅   | Filter la liste des produits par le nom                                                                   |                6                 | La liste des produits s'update en entrant quelque chose dans la barre de recherche.                               | Faire qu'elle update correctement en prenant en compte ce que le nom contient et non est.     |
| E1  | MUST     |   🟦   | Mettre le code sur GitHub page.                                                                           | Demander mais pas dans un récit. | On peut accèder le site sur Github Page.                                                                          | Difficulter à initialiser sur Github page.                                                    |

```

```
