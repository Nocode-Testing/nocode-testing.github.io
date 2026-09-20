---
id: REFERENTIEL-EXIGENCES
statut: brouillon
---

# Referentiel des exigences

Ce referentiel ne contient que des exigences explicitement confirmees par le commanditaire. A sa creation, aucune nouvelle exigence metier n'est ajoutee : les besoins existants restent a transformer et a valider increment par increment.

## Regles de gestion

- Une exigence est identifiee par `REQ-<numero>` et est ajoutee avant ou en meme temps que ses US.
- Le commanditaire valide seul la priorite et toute exception. Les agents proposent une priorite et consignent leur justification.
- Une exigence dont le lot n'est pas valide reste `brouillon` ou `a_revoir`.
- Une US d'interface ne peut etre liee qu'apres validation explicite du lot UI correspondant.
- Chaque exigence lie ses US, les exigences non fonctionnelles applicables et les references GitHub utiles.

## Champs obligatoires

| Champ | Description |
|---|---|
| Identifiant | `REQ-<numero>`, unique et non reutilisable. |
| Description | Besoin verifiable, sans prescrire de solution non validee. |
| Source / justification | Decision, besoin ou echange date et identifie. |
| Priorite | `proposee` puis valeur validee par le commanditaire. |
| Statut | Statut commun defini dans le README. |
| Exigences non fonctionnelles | Securite, accessibilite, RGPD, charge, performance, recette ou deploiement si applicables. |
| US concernees | Identifiants `US-*` et liens vers les fichiers. |
| References externes | GitHub Issue et/ou Project si existants. |

## Entrees

Aucune entree REQ n'est creee par ce chantier documentaire.