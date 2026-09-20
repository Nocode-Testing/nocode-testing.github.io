---
id: CATALOGUE-CT
statut: brouillon
---

# Cas de test

Un cas de test est stocke dans `CT-<numero>-<slug-court>.md` et derive d'un ou plusieurs criteres d'acceptation d'une US.

## Modele minimal

```markdown
---
id: CT-001
statut: brouillon
liens:
  user_stories:
    - US-001
  requirements:
    - REQ-001
---

# CT-001 - Titre

## Objectif

## Preconditions

## Donnees de test

## Etapes et resultats attendus

## Type

Manuel, automatise, integration, E2E, securite ou accessibilite.
```

Les donnees de test sont fictives ou anonymisees. Un CT lie explicitement les `REQ-*` et `US-*` couverts afin de permettre le chainage.

## Entrees

Aucun cas de test n'est cree par ce chantier documentaire.