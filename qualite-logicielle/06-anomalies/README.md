---
id: CATALOGUE-ANOM
statut: brouillon
---

# Anomalies

La source de gestion des anomalies est [GitHub Project #1](https://github.com/orgs/Nocode-Testing/projects/1/views/1), avec une GitHub Issue par anomalie lorsque celle-ci est creee. Ce dossier fournit l'index de tracabilite et ne duplique pas les details de l'issue.

## Modele minimal

```markdown
---
id: ANOM-001
statut: brouillon
liens:
  github_issue: null
  github_project: https://github.com/orgs/Nocode-Testing/projects/1/views/1
  executions:
    - EXEC-001
---

# ANOM-001 - Titre court

## Resume et impact

## Reproduction

## Priorite proposee

## Priorite validee par le commanditaire

## Statut GitHub
```

Les agents peuvent creer ou proposer une anomalie selon leurs autorisations, mais ne valident jamais sa priorite. Les anomalies bloquantes ou majeures, ainsi que les violations axe critiques ou serieuses non justifiees, interdisent la promotion en production. Les exceptions restent soumises au commanditaire.

## Entrees

Aucune anomalie ni GitHub Issue n'est creee par ce chantier documentaire.