# Handoff

Ce document sert de memoire de contexte compacte pour un LLM intervenant sur ce projet.
Il doit permettre de comprendre rapidement le projet, ses contraintes, ses priorites et l'etat courant sans dependre d'une session de chat longue.

## Objectif du projet
- Concevoir et publier le futur site de `nocode-testing.com` apres le retrait de l'ancienne base Docusaurus.
- Le type de site, le contenu initial, les fonctionnalites et les objectifs de mise en ligne restent a confirmer dans `build-app.md`.

## Stack et architecture
- Node.js >= 18 est declare dans `package.json`.
- Aucune stack frontend, backend, base de donnees, outil de build ou outil de test n'est encore retenu.
- GitHub Pages est la cible historique de publication, mais sa reconfiguration n'est pas encore confirmee.

## Structure importante
- `README.md` : presentation et statut du depot.
- `handoff.md` : memoire de contexte technique.
- `handoff_UI.md` : memoire de contexte UX/UI.
- `build-app.md` : questions, decisions et recommandations de pilotage.
- `.github/agents/` : definitions des agents specialises et de Dominion Orchestrateur.

## Commandes utiles
- Installation: `npm install`
- Developpement local: non defini (le script `start` n'existe pas encore).
- Tests, lint, build et controle de types: non definis.

## Conventions du projet
- Aucun framework n'est impose : Camity Front privilegie JavaScript natif lorsque le besoin le permet.
- Les decisions techniques, conventions durables et impacts d'architecture doivent etre reportes dans ce fichier.
- Les contrats API sont sous la responsabilite de Rindel Dev ; les decisions infrastructure et de deploiement sous celle de Soso ArchiOps.
- Dominion coordonne les agents et attend la validation explicite du commanditaire avant chaque chantier.

## Priorites techniques
- Performance.
- Simplicite du code.
- Documentation maintenue a jour.
- Securite applicative et bonnes pratiques de cybersecurity.

## Points d'attention
- Les informations de cadrage dans `build-app.md` restent sans reponse : elles bloquent le choix de stack, d'hebergement, de contenu, de design et de strategie de test.
- Aucun code applicatif, dependance, verrou de dependances, pipeline CI/CD ou configuration de deploiement n'est present a ce stade.

## Travaux en cours
- Revue des agents et mise a jour de la documentation de demarrage terminees le 2026-09-13.
- Cadrage fonctionnel et technique en attente des reponses du commanditaire.

## Prochaines etapes
- Repondre aux questions de cadrage de `build-app.md`.
- Faire valider par le commanditaire le premier lot de travail avant de deleguer a Scarce PO, Soso ArchiOps ou Armindia UI.

## Historique utile
- L'ancienne base Docusaurus a ete retiree ; le depot repart d'une base propre.