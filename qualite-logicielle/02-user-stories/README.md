---
id: CATALOGUE-US
statut: brouillon
---

# User stories

Une user story est stockee dans un fichier `US-<numero>-<slug-court>.md`. Aucun fichier US n'est cree tant qu'un besoin limite et son exigence parente ne sont pas confirmes.

## Modele minimal

```markdown
---
id: US-001
statut: brouillon
liens:
  requirements:
    - REQ-001
  github_issue: null
---

# US-001 - Titre

En tant que ...
Je veux ...
Afin de ...

## Contexte

## Regles metier

## Criteres d'acceptation

```gherkin
Scenario: Nom du scenario
  Given ...
  When ...
  Then ...
```

## Exigences non fonctionnelles

## Avis et decisions

## Liens
```

## Regles de maturite

- Toute nouvelle US est relue par Mina Cybersecurite avant le statut `pret`.
- Mikaya test challenge les criteres d'acceptation. Camity Front, Rindel Dev et Soso ArchiOps sont sollicites selon les impacts frontend, backend, architecture, charge, donnees, deploiement ou exploitation.
- Une US est decoupee si elle ne tient pas dans un cycle court ou si elle couvre plusieurs resultats independants.
- Une US d'interface reste `brouillon` tant que le lot UI n'est pas valide par le commanditaire.
- La priorite et les exceptions sont proposees par les agents, puis validees exclusivement par le commanditaire.

## Entrees

Aucune US n'est creee par ce chantier documentaire.