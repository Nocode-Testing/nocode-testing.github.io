---
id: CATALOGUE-CAMP
statut: brouillon
---

# Campagnes de test

Une campagne est stockee dans `CAMP-<numero>-<slug-court>.md`. Elle selectionne des cas de test pour une version, un environnement et un objectif definis.

## Modele minimal

```markdown
---
id: CAMP-001
statut: brouillon
liens:
  test_cases:
    - CT-001
  github_project: https://github.com/orgs/Nocode-Testing/projects/2/views/1?system_template=kanban
---

# CAMP-001 - Titre

## Objectif et perimetre

## Version et environnement

## Cas selectionnes

## Criteres d'entree

## Criteres de sortie

## Risques et exceptions proposees
```

Une campagne de recette ou de production identifie le commit ou la version testee. Toute exception est soumise a la validation du commanditaire. Une promotion n'est jamais autorisee par un agent ni par le seul resultat de campagne.

## Entrees

Aucune campagne n'est creee par ce chantier documentaire.