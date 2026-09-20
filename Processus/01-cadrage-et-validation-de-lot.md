# 01 - Cadrage et validation de lot

## Objectif

Transformer un besoin limite en increment livrable sans demarrer de travaux hors perimetre.

## Entrees

- Besoin formule par le sponsor.
- Contexte : `README.md`, `handoff.md`, `handoff_UI.md`, `build-app.md` et `pilotage-projet.md`.

## Etapes

1. Dominion reformule le besoin, le resultat attendu et les exclusions.
2. Les agents concernes identifient dependances, risques, donnees, securite, tests et impacts d'exploitation.
3. Le lot indique : perimetre, responsable, criteres d'acceptation, preuves attendues, strategie de recette et retour arriere.
4. Les questions capables de modifier l'architecture ou la conformite sont isolees comme bloquantes.
5. Le sponsor valide explicitement le lot. Sans cette validation, aucun chantier applicatif ou distant ne commence.
6. Dominion inscrit le statut du lot dans `pilotage-projet.md` et les decisions durables dans les handoffs ou un ADR.

## Point de controle

Le lot est pret si un tiers peut identifier le commit attendu, les tests, le responsable de validation et la condition de sortie.

## Exception et retour arriere

Toute reduction de perimetre, derogation de qualite ou exception de calendrier est soumise au sponsor. Si le lot est invalide, il est remis a l'etat a cadrer ; aucun travail non valide n'est promu.