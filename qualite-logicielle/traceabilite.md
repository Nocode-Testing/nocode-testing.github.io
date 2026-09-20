---
id: MATRICE-TRACEABILITE
statut: brouillon
---

# Matrice de traceabilite

La chaine de preuve est : `REQ -> US -> CT -> CAMP -> EXEC -> ANOM`.

| REQ | US | CT | CAMP | EXEC | ANOM | Etat de couverture |
|---|---|---|---|---|---|---|
| Aucune entree | Aucune entree | Aucune entree | Aucune entree | Aucune entree | Aucune entree | Referentiel initialise sans besoin ajoute |

## Regles de chainage

- Chaque `US-*` reference au moins un `REQ-*` parent.
- Chaque `CT-*` reference les `US-*` et `REQ-*` qu'il couvre.
- Chaque `CAMP-*` liste les `CT-*` executes.
- Chaque `EXEC-*` reference une campagne, un commit ou une version et son environnement.
- Chaque `ANOM-*` reference l'execution qui l'a revelee quand elle est connue, ainsi que sa GitHub Issue et Project #1.
- Project #2 peut etre lie aux US ou campagnes pour le suivi Kanban, sans remplacer la matrice.

## Liens GitHub

- Anomalies : [GitHub Project #1](https://github.com/orgs/Nocode-Testing/projects/1/views/1).
- Kanban : [GitHub Project #2](https://github.com/orgs/Nocode-Testing/projects/2/views/1?system_template=kanban).
- Issues : ajouter le lien de l'issue creee dans le front matter de l'US ou de l'anomalie. Aucun lien d'issue n'est invente avant sa creation.