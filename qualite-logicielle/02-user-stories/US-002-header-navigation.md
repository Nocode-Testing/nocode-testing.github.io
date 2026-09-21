---
id: US-002
statut: a_revoir
liens:
  requirements:
    - REQ-002
  github_issue: null
  github_project: null
---

# US-002 - Header et navigation

En tant que visiteur,
Je veux trouver le logo et les rubriques principales dans le header,
Afin de naviguer rapidement dans le site.

## Contexte

Le menu est rattache au header et positionne a droite selon la maquette. Le logo source clair est `assets/brand/Logo_NCT_vectoriel.svg`; le logo du theme sombre est `assets/brand/Logo_NCT_vectoriel_blanc.png`. Aucun des deux ne doit etre recompose.

## Regles metier

- La navigation expose Blog (`/blog/`), Labo Test & IA (`/labo-test-ia/`), Ressources (`/ressources/`), A propos (`/a-propos/`) et Contact (`/contact/`).
- Le logo est adapte au theme courant : `assets/brand/Logo_NCT_vectoriel.svg` en clair/couleur et `assets/brand/Logo_NCT_vectoriel_blanc.png` en sombre ; son nom accessible identifie la marque et son lien cible une page valide.
- Le menu fonctionne sur desktop et mobile. Sur mobile, son bouton natif expose `aria-expanded` et `aria-controls`.

## Criteres d'acceptation

```gherkin
Scenario: Afficher le header et ses rubriques
  Given un visiteur ouvre une page du lot MVP
  When le header est rendu
  Then le logo de reference est visible
  And le logo a un nom accessible identifiant nocode-testing
  And les rubriques Blog, Labo Test & IA, Ressources, A propos et Contact sont accessibles avec leurs routes valides
  And le menu est rattache au header et place a droite sur desktop

Scenario: Naviguer au clavier
  Given un visiteur utilise uniquement le clavier
  When il parcourt le header
  Then chaque lien a un nom accessible
  And le focus est visible
  And chaque lien peut etre active avec Entree

Scenario: Utiliser le menu sur mobile
  Given un viewport mobile
  When le visiteur ouvre le menu
  Then les rubriques restent accessibles sans debordement horizontal
  And le bouton natif expose `aria-expanded="true"` et `aria-controls` vers le menu
  And la fermeture du menu est accessible au clavier avec Echap
  And le focus revient au bouton d'ouverture apres fermeture avec Echap
  And la navigation ne cree pas de piege clavier

Scenario: Adapter le logo au theme
  Given le visiteur consulte le site en theme clair puis en theme sombre
  When le header est rendu
  Then le logo clair/couleur est utilise en theme clair
  And le logo blanc est utilise en theme sombre
  And le logo conserve un nom accessible dans les deux themes
```

## Exigences non fonctionnelles

- Elements semantiques et noms accessibles ; ARIA complete le HTML natif.
- Cibles interactives d'au moins 44 x 44 px et contrastes suffisants dans les deux themes.
- Aucun secret ni donnee personnelle dans le header, les logs ou les attributs de test.
- Verification Chrome/Firefox, recette et CI bloquante sur build/tests.

## Avis et decisions

- Taille : OK pour un cycle court, limitee au header et a la navigation.
- Revues Mina Cybersecurite, Mikaya test et Camity Front attendues avant `pret`.
- Statut de revue : `a_revoir`.

## Liens

- Exigence parente : [REQ-002](../01-exigences/referentiel-exigences.md#req-002---header-et-navigation)
- Maquette : `assets/mockups/accueil-puzzle-ateliers-themes.svg`
- GitHub Issue : `null`
