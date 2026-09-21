---
id: US-003
statut: a_revoir
liens:
  requirements:
    - REQ-003
  github_issue: null
  github_project: null
---

# US-003 - Theme clair et sombre

En tant que visiteur,
Je veux choisir entre un theme clair et un theme sombre,
Afin de consulter le site dans des conditions visuelles adaptees a mes preferences.

## Contexte

Le controle de theme est une icone seule visuellement, mais son nom et son etat sont exposes aux technologies d'assistance. Les deux themes possedent leurs propres jetons.

La persistance utilise la cle `nct-theme` et uniquement les valeurs `light` ou `dark`. Le choix enregistre prime sur la preference systeme, puis le theme clair est le repli.

## Regles metier

- En clair, le controle porte le nom « Passer au mode sombre » et affiche une lune.
- En sombre, il porte le nom « Passer au mode clair » et affiche un soleil.
- Sans choix enregistre, la preference systeme est respectee au premier chargement.
- Un choix explicite est conserve localement sous `nct-theme`, sans traceur ni donnee personnelle.
- Seules les valeurs `light` et `dark` sont valides ; toute autre valeur est ignoree puis supprimee du stockage.

## Criteres d'acceptation

```gherkin
Scenario: Basculer du theme clair au theme sombre
  Given le site est en theme clair
  When le visiteur active le controle de theme
  Then le site passe en theme sombre
  And le controle expose l'etat sombre et le nom « Passer au mode clair »
  And le focus reste visible

Scenario: Respecter la preference systeme sans choix enregistre
  Given aucun choix de theme n'est enregistre
  And la preference systeme est sombre
  When le visiteur charge le site
  Then le site est affiche en theme sombre

Scenario: Resoudre le theme dans l'ordre defini
  Given un choix `light` ou `dark` est enregistre sous `nct-theme`
  And la preference systeme est differente
  When le visiteur charge le site
  Then le choix enregistre est applique avant la preference systeme
  And si aucun choix valide n'est enregistre la preference systeme est appliquee
  And le theme clair est applique si aucun choix valide ni preference sombre n'existe

Scenario: Ignorer une valeur de stockage invalide
  Given `nct-theme` contient une valeur autre que `light` ou `dark`
  When le visiteur charge le site
  Then la valeur invalide est ignoree et supprimee
  And le theme est resolu selon la preference systeme puis le clair par defaut

Scenario: Persister un choix explicite
  Given le visiteur a choisi le theme sombre
  When il recharge le site
  Then le theme sombre est conserve
  And aucune donnee personnelle ni traceur non essentiel n'est utilise
  And la navigation vers une autre page conserve le theme sombre

Scenario: Utiliser le controle au clavier et avec un lecteur d'ecran
  Given un visiteur utilise le clavier ou un lecteur d'ecran
  When il atteint le controle de theme
  Then son nom et son etat sont comprehensibles
  And il peut le basculer avec l'activation native du controle
  And le focus visible est conserve apres activation
```

## Exigences non fonctionnelles

- Contrastes, focus et lisibilite verifies dans les deux themes.
- L'information ne repose jamais sur la couleur seule et la cible mesure au moins 44 x 44 px.
- Verification Chrome/Firefox, tests de preference/persistance, recette et CI bloquante.
- Le stockage local est documente dans la politique de confidentialite si l'analyse juridique le requiert.

## Avis et decisions

- Taille : OK pour un cycle court, limitee au controle et aux tokens de theme.
- Revues Mina Cybersecurite, Mikaya test et Camity Front attendues avant `pret`.
- Statut de revue : `a_revoir`.

## Liens

- Exigence parente : [REQ-003](../01-exigences/referentiel-exigences.md#req-003---theme-clair-et-sombre)
- Maquette : `assets/mockups/accueil-puzzle-ateliers-themes.svg`
- GitHub Issue : `null`
