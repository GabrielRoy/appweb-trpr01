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

|  ID | Priorité | Statut | Titre (tâche) | Relié à (RU#) | Critères d’acceptation (définition de done) | Notes / obstacles |
| --: | :------: | :----: | ------------- | :-----------: | ------------------------------------------- | ----------------- |
|     |          |        |               |               |                                             |                   |
| A1  |   MUST   |   🟦   |End MainPage.vue|Base d'un site| La page affiche.                             |                   |
| B1  |   MUST   |	 ✅   |Finir et implémenter le formulaire pour qu'il intéragisse avec le site|Le formulaire affiche et fonctionne pour la modification et création. | 2 et 1                                             |                   |
| B2    |  MUST  |   ✅   |Finir l'affichage du produit un fois cliqué. | 7             |                                             |                   |
| C1    | MUST     |  🟦    | Implémentation du supprimage              |  4             |                                             |                   |
| C2  | MUST     |  ✅    | Afficher un produit                        |  7             | Le produit sélectionné apparaît correctement avec toutes ses informations |                   |
| C3  | MUST     |  ✅    | Affichage en temps réel des quantités avec indicateur visuel | 8 | Les quantités se mettent à jour immédiatement et les couleurs changent selon la quantité (ex: vert, jaune, rouge) |                   |
| C4  | MUST     |  ✅    | Notification lorsqu'un produit atteint un stock critique| 9 | Un message apparaît sous la liste indiquant tous les produits en stock critique |                   |
| C3  | MUST     | 🟦     | Bouton "Dupliquer" qui préremplit un nouveau formulaire avec les données du produit sélectionné | 3             | - le formulaire de création se remplit avec les données du produit.seule la préremplissage est fait. | 
