---
id: REFERENTIEL-EXIGENCES
statut: a_revoir
---

# Referentiel des exigences

Ce referentiel ne contient que des exigences explicitement confirmees par le commanditaire. A sa creation, aucune nouvelle exigence metier n'est ajoutee : les besoins existants restent a transformer et a valider increment par increment.

## Regles de gestion

- Une exigence est identifiee par `REQ-<numero>` et est ajoutee avant ou en meme temps que ses US.
- Le commanditaire valide seul la priorite et toute exception. Les agents proposent une priorite et consignent leur justification.
- Une exigence dont le lot n'est pas valide reste `brouillon` ou `a_revoir`.
- Une US d'interface ne peut etre liee qu'apres validation explicite du lot UI correspondant.
- Chaque exigence lie ses US, les exigences non fonctionnelles applicables et les references GitHub utiles.

## Champs obligatoires

| Champ | Description |
|---|---|
| Identifiant | `REQ-<numero>`, unique et non reutilisable. |
| Description | Besoin verifiable, sans prescrire de solution non validee. |
| Source / justification | Decision, besoin ou echange date et identifie. |
| Priorite | `proposee` puis valeur validee par le commanditaire. |
| Statut | Statut commun defini dans le README. |
| Exigences non fonctionnelles | Securite, accessibilite, RGPD, charge, performance, recette ou deploiement si applicables. |
| US concernees | Identifiants `US-*` et liens vers les fichiers. |
| References externes | GitHub Issue et/ou Project si existants. |

## Entrees

### REQ-001 - Accueil et panneaux puzzle

| Champ | Valeur |
|---|---|
| Identifiant | `REQ-001` |
| Description | L'accueil du MVP presente le titre initial « La Qualité logicielle est l'affaire de tou•te•s », les CTA « L'univers du Testeur du Granier » et « Nos experimentations », ainsi que les quatre panneaux puzzle nommes Question, Essai, Retour terrain et Partage, dans cet ordre. Les CTA ciblent `/blog/` et `/labo-test-ia/`. |
| Source / justification | Arbitrages sponsor et revues Mina/Mikaya consignes en `build-app.md`, sections 7.19-7.20, le 2026-09-21 ; maquette `assets/mockups/accueil-puzzle-ateliers-themes.svg` ; `handoff_UI.md`. |
| Priorite | `haute`, validee par le commanditaire le 2026-09-21. |
| Statut | `a_revoir` |
| Exigences non fonctionnelles | Accessibilite clavier et lecteur d'ecran, ordre de lecture semantique, contrastes applicables WCAG 2.2 AA, responsive, performance statique, Chrome/Firefox, recette et CI bloquante. |
| US concernees | [US-001](../02-user-stories/US-001-accueil-panneaux-puzzle.md) |
| References externes | GitHub Issue: `null`; GitHub Project: `null` |

### REQ-002 - Header et navigation

| Champ | Valeur |
|---|---|
| Identifiant | `REQ-002` |
| Description | Le header affiche le logo de reference adapte au theme, rattache le menu a droite et expose Blog (`/blog/`), Labo Test & IA (`/labo-test-ia/`), Ressources (`/ressources/`), A propos (`/a-propos/`) et Contact (`/contact/`). Il fonctionne sur desktop et mobile avec un menu natif accessible. |
| Source / justification | Arbitrages sponsor et revues Mina/Mikaya consignes en `build-app.md`, sections 7.19-7.20, le 2026-09-21 ; maquette `assets/mockups/accueil-puzzle-ateliers-themes.svg` ; `handoff_UI.md`. |
| Priorite | `haute`, validee par le commanditaire le 2026-09-21. |
| Statut | `a_revoir` |
| Exigences non fonctionnelles | HTML semantique, navigation clavier, focus visible, noms accessibles, cibles d'au moins 44 x 44 px, contrastes, responsive, Chrome/Firefox, recette et CI. |
| US concernees | [US-002](../02-user-stories/US-002-header-navigation.md) |
| References externes | GitHub Issue: `null`; GitHub Project: `null` |

### REQ-003 - Theme clair et sombre

| Champ | Valeur |
|---|---|
| Identifiant | `REQ-003` |
| Description | Le site propose deux themes brandes, `light` et `dark`, selectionnables depuis le header par une icone seule visuellement avec nom accessible et etat expose. La cle `nct-theme` conserve un choix valide ; la resolution suit choix enregistre, preference systeme, puis clair par defaut. |
| Source / justification | Arbitrages sponsor et revues Mina/Mikaya consignes en `build-app.md`, sections 7.19-7.20, le 2026-09-21 ; maquette `assets/mockups/accueil-puzzle-ateliers-themes.svg` ; `handoff_UI.md`. |
| Priorite | `haute`, validee par le commanditaire le 2026-09-21. |
| Statut | `a_revoir` |
| Exigences non fonctionnelles | Contrastes et focus dans les deux themes, clavier et lecteur d'ecran, aucune information par la couleur seule, stockage sans donnee personnelle ni traceur, Chrome/Firefox, tests, recette et CI. |
| US concernees | [US-003](../02-user-stories/US-003-theme-clair-sombre.md) |
| References externes | GitHub Issue: `null`; GitHub Project: `null` |

### REQ-004 - Footer legal et RGPD

| Champ | Valeur |
|---|---|
| Identifiant | `REQ-004` |
| Description | Le footer present sur toutes les pages du lot rend accessibles les mentions legales (`/mentions-legales/`), la politique de confidentialite (`/confidentialite/`), les informations RGPD et le lien LinkedIn du perimetre MVP, sans analytics, publicite, suivi ni script tiers non justifie. Les adresses sont `contact@nocode-testing.com` et `rgpd@nocode-testing.com`. |
| Source / justification | Arbitrages sponsor et revues Mina/Mikaya consignes en `build-app.md`, sections 7.19-7.20, le 2026-09-21 ; `README.md`, `handoff.md`, `pilotage-projet.md` et processus RGPD. |
| Priorite | `haute`, validee par le commanditaire le 2026-09-21. |
| Statut | `a_revoir` |
| Exigences non fonctionnelles | Information accessible, liens clavier/mobile, minimisation des donnees, HTTPS, Chrome/Firefox, relecture juridique humaine avant publication, recette et CI. |
| US concernees | [US-004](../02-user-stories/US-004-footer-legal-rgpd.md) |
| References externes | GitHub Issue: `null`; GitHub Project: `null` |

### REQ-005 - Formulaire de contact fonctionnel

| Champ | Valeur |
|---|---|
| Identifiant | `REQ-005` |
| Description | La route `/contact/` permet de saisir et transmettre une demande avec les champs `nom`, `e-mail`, `societe`, `sujet` et `message`. Le transport est configurable selon l'environnement : local sans secret SMTP commite, recette avec donnees fictives et destinataire `test_recette@nocode-testing.com`, production avec SMTP OVH et destinataire `contact@nocode-testing.com`. Le traitement applique une validation serveur, un honeypot, une limitation de debit durable et Turnstile uniquement en production. |
| Source / justification | Decision du commanditaire le 2026-09-21 ; `build-app.md`, section 7.22 ; `handoff.md` ; `Processus/09-formulaire-contact-et-messagerie.md` ; `Processus/11-projet-politique-confidentialite.md`. |
| Priorite | `haute`, validee par le commanditaire le 2026-09-21. |
| Statut | `a_revoir` |
| Exigences non fonctionnelles | Validation serveur et encodage sur fonction same-origin, erreurs generiques, honeypot, limitation de debit durable, verification serveur Turnstile en production, absence de secrets dans Git/logs, minimisation des logs, HTTPS en recette et production, donnees fictives en recette, confidentialite et duree de conservation conforme a la politique a relire juridiquement, WCAG 2.2 AA applicable, performance et charge a qualifier, recette SMTP bloquante avant production, CI et promotion humaine. |
| US concernees | [US-005](../02-user-stories/US-005-formulaire-contact.md) |
| References externes | GitHub Issue: `null`; GitHub Project: `null` |