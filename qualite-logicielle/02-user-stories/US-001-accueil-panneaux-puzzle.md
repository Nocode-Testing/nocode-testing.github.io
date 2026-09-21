---
id: US-001
statut: a_revoir
liens:
  requirements:
    - REQ-001
  github_issue: null
  github_project: null
---

# US-001 - Accueil et panneaux puzzle

En tant que visiteur de nocode-testing.com,
Je veux comprendre l'univers du site depuis l'accueil et accéder à ses deux premiers parcours,
Afin de consulter le contenu du Testeur du Granier ou les expérimentations.

## Contexte

Le premier incrément reprend `assets/mockups/accueil-puzzle-ateliers-themes.svg`. Le titre initial est « La Qualité logicielle est l'affaire de tou•te•s ». Les quatre panneaux puzzle sont nommes, dans l'ordre de lecture, Question, Essai, Retour terrain et Partage. Ce sont des reperes de composition et non des controles lorsqu'ils sont decoratifs.

## Regles metier

- Les CTA affichent exactement « L'univers du Testeur du Granier » et « Nos experimentations ».
- Le CTA « L'univers du Testeur du Granier » cible `/blog/` et le CTA « Nos experimentations » cible `/labo-test-ia/`.
- Les quatre panneaux sont repris dans l'ordre Question, Essai, Retour terrain, Partage, sans concurrencer les contenus ni les controles ; s'ils sont decoratifs, ils ne sont pas exposes comme des controles.
- Le titre variable a terme et les themes sponsorises sont hors de cette US.

## Criteres d'acceptation

```gherkin
Scenario: Afficher le contenu principal de l'accueil
  Given un visiteur ouvre la page d'accueil
  When la page est rendue
  Then le titre « La Qualité logicielle est l'affaire de tou•te•s » est visible
  And les CTA « L'univers du Testeur du Granier » et « Nos experimentations » sont visibles
  And les quatre panneaux puzzle sont nommes Question, Essai, Retour terrain et Partage dans cet ordre
  And les panneaux decoratifs ne sont pas exposes comme des controles

Scenario: Verifier les destinations des CTA
  Given un visiteur ouvre la page d'accueil
  When il active le CTA « L'univers du Testeur du Granier » puis le CTA « Nos experimentations »
  Then le premier parcours ouvre `/blog/`
  And le second parcours ouvre `/labo-test-ia/`
  And chaque destination correspond a une page valide

Scenario: Utiliser les CTA au clavier
  Given un visiteur navigue avec le clavier
  When il atteint un CTA et l'active avec Entree
  Then le parcours cible est ouvert
  And le focus reste visible

Scenario: Consulter l'accueil sur petit ecran
  Given un viewport de `320x568`, `375x667`, `768x1024` ou `1280x800`
  When la page est rendue
  Then aucun contenu n'est tronque ni superpose
  And chaque CTA reste lisible sans troncature et sans depasser trois lignes
  And chaque destination de CTA reste utilisable
```

## Exigences non fonctionnelles

- HTML semantique, ordre de lecture coherent et texte utile pour les lecteurs d'ecran.
- Contrastes et focus visibles conformes aux objectifs WCAG 2.2 AA applicables.
- Verification Chrome/Firefox, recette avant promotion et CI bloquante sur build/tests.

## Avis et decisions

- Taille : OK pour un cycle court, limitee a l'accueil et aux panneaux.
- Revues Mina Cybersecurite, Mikaya test et Camity Front attendues avant `pret`.
- Statut de revue : `a_revoir`.

## Liens

- Exigence parente : [REQ-001](../01-exigences/referentiel-exigences.md#req-001---accueil-et-panneaux-puzzle)
- Maquette : `assets/mockups/accueil-puzzle-ateliers-themes.svg`
- GitHub Issue : `null`
