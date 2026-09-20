---
id: CATALOGUE-EXEC
statut: brouillon
---

# Executions de test

Une execution est stockee dans `EXEC-<numero>-<slug-court>.md` et enregistre le resultat d'une campagne sur un commit et un environnement identifies.

## Modele minimal

```markdown
---
id: EXEC-001
statut: en_cours
liens:
  campaign: CAMP-001
  anomalies: []
---

# EXEC-001 - Titre

## Version, commit et environnement

## Date et executant

## Resultats par cas

## Anomalies detectees

## Decision proposee

## Decision du commanditaire
```

Les resultats possibles sont `reussi`, `echoue`, `bloque` ou `annule`. Les anomalies sont liees par leur identifiant `ANOM-*` et par leur GitHub Issue. Seul le commanditaire consigne la validation de recette, une exception acceptee ou une promotion production.

## Entrees

Aucune execution n'est creee par ce chantier documentaire.