# Handoff

Ce document sert de memoire de contexte compacte pour un LLM intervenant sur ce projet.
Il doit permettre de comprendre rapidement le projet, ses contraintes, ses priorites et l'etat courant sans dependre d'une session de chat longue.

## Objectif du projet
- Concevoir et publier le futur site de `nocode-testing.com` apres le retrait de l'ancienne base Docusaurus.
- Le MVP est une vitrine comprenant accueil, navigation, blog "Le testeur du granier" avec un premier article, experimentations IA, ressources, a propos, contact, footer RGPD et lien LinkedIn.
- Les evolutions hors MVP envisagées sont des micro-applications JavaScript, des quiz, un forum et des commentaires.

## Stack et architecture
- Node.js 22 LTS est la version cible du MVP, declaree dans `package.json`.
- Le MVP publie les articles depuis Markdown versionne dans Git. Eleventy est valide pour le MVP afin de generer le HTML, avec CSS et JavaScript natif ; ce choix ne requiert pas de base de donnees.
- Les routes MVP validees sont `/blog/`, `/labo-test-ia/`, `/ressources/`, `/a-propos/`, `/contact/`, `/mentions-legales/` et `/confidentialite/`.
- Une base de donnees et un backoffice authentifie ne seront instruits que lorsque plusieurs editeurs, des droits d'acces ou une edition web seront justifies ; aucun CMS externe ne sera utilise.
- Les changements applicatifs comme editoriaux passent par recette. Un contenu urgent peut suivre un circuit accelere, mais reste une PR, un build, une recette et une promotion humaine d'un commit identifie ; aucune modification manuelle non tracee en production.
- Le premier lot produit couvre l'accueil, le header, le theme clair/sombre et le footer legal/RGPD. La personnalisation de themes brandes par sponsors ou outils est reportee apres le MVP.
- GitHub heberge le code et Vercel est la cible de deploiement. Deux environnements HTTPS sont requis : recette protegee et production publique. Le sous-domaine stable `recette.nocode-testing.com` est souhaite ; son parametrage exigera un CNAME web OVH sans modifier les DNS e-mail.
- Le domaine `nocode-testing.com` est controle par le commanditaire, qui peut modifier sa configuration DNS pour Vercel.
- La promotion production est exclusivement humaine. GitHub Actions est recommande pour les controles ; le deploiement Vercel de production doit etre stage puis promu manuellement apres validation de recette.

## Structure importante
- `README.md` : presentation et statut du depot.
- `handoff.md` : memoire de contexte technique.
- `handoff_UI.md` : memoire de contexte UX/UI.
- `build-app.md` : questions, decisions et recommandations de pilotage.
- `.github/agents/` : definitions des agents specialises et de Dominion Orchestrateur.
- `assets/brand/` : logos et charte graphique de reference. Variantes disponibles : couleur (`Logo_NCT_vectoriel.svg` et PNG), noir et blanc (`Logo_NCT_vectoriel_NB.svg` et PNG), blanc (PNG) et charte graphique PDF.
- `assets/mockups/` : maquettes SVG accueil/header, dont `accueil-atelier-calibre.svg` recommandee.

## Commandes utiles
- Installation: `npm install`
- Developpement local: non defini (le script `start` n'existe pas encore).
- Tests, lint, build et controle de types: non definis.

## Conventions du projet
- Aucun framework n'est impose : Camity Front privilegie JavaScript natif lorsque le besoin le permet.
- Les decisions techniques, conventions durables et impacts d'architecture doivent etre reportes dans ce fichier.
- Les contrats API sont sous la responsabilite de Rindel Dev ; les decisions infrastructure et de deploiement sous celle de Soso ArchiOps.
- Dominion coordonne les agents et attend la validation explicite du commanditaire avant chaque chantier.
- Le travail est incremental : besoin partage avec Dominion, lot cadre et valide, implementation limitee au lot, deploiement en recette, validation, promotion en production et validation finale.
- Viser les principes WCAG 2.2 AA applicables : semantique HTML, clavier, focus visible, contrastes, libelles et alternatives utiles ; ARIA complete le HTML natif, sans le remplacer.
- Appliquer la minimisation des donnees, le consentement des traceurs non essentiels, une information RGPD claire et l'absence de secrets ou donnees personnelles inutiles dans les logs.

## Priorites techniques
- Performance.
- Simplicite du code.
- Documentation maintenue a jour.
- Securite applicative et bonnes pratiques de cybersecurity.

## Points d'attention
- La stack MVP Eleventy + HTML/CSS/JavaScript natif + Node.js 22 LTS est validee. La direction visuelle de reference MVP est `assets/mockups/accueil-puzzle-ateliers-themes.svg`.
- Le theme utilise `nct-theme` avec `light` et `dark`. L'ordre de resolution est choix enregistre, preference systeme, puis clair par defaut. Le logo sombre est `assets/brand/Logo_NCT_vectoriel_blanc.png`.
- Le formulaire de contact doit transmettre `nom`, `e-mail`, `societe`, `sujet` et `message` a `contact@nocode-testing.com`. La recette utilise uniquement `test_recette@nocode-testing.com` et l'adresse publique RGPD est `rgpd@nocode-testing.com`.
- Le formulaire `/contact/` est fonctionnel dans le MVP. En local, `CONTACT_TRANSPORT=fake` est le défaut ; `CONTACT_TRANSPORT=smtp` peut être choisi explicitement avec des variables SMTP de session non commitées. En recette, l'essai SMTP OVH utilise `test_recette@nocode-testing.com` ; en production, l'envoi vise `contact@nocode-testing.com`.
- Le footer affiche deux liens LinkedIn distincts : personnel `https://www.linkedin.com/in/michael-granier/` et entreprise `https://www.linkedin.com/company/nocode-testing`.
- SMTP OVH est la piste privilegiee, sans changement DNS prevu. Le formulaire peut etre concu avec l'hypothese que SMTP fonctionne ; sa connectivite TLS depuis Vercel, ses quotas et sa delivrabilite seront verifies par un essai controle en recette apres deploiement. Un echec declenche l'etude d'une alternative API HTTPS. Les identifiants ne doivent jamais etre verses dans Git ou la conversation.
- Antispam attendu : validation serveur, honeypot, limitation de debit durable et Cloudflare Turnstile non invasif en production seulement. Turnstile est valide sous reserves : mode Managed/intervention a la demande, verification serveur Siteverify obligatoire, restriction aux hotes production, refus securise en cas d'indisponibilite et revue juridique de son DPA/transferts. La recette n'active pas le CAPTCHA pour garantir les E2E automatises.
- La protection Vercel est retenue pour la recette et les previews. Une protection par mot de passe implique a priori Vercel Pro ; le plan et les personnes autorisees restent a confirmer.
- Les anomalies vivent dans GitHub Issues/Project #1 avec priorite proposee par les agents et priorite validee exclusivement par un humain. Les anomalies bloquantes/majeures et les violations axe critiques/serieuses non justifiees interdisent toute production.
- Le commanditaire est l'unique administrateur de Vercel, GitHub, OVH/DNS et secrets, ainsi que l'unique validateur des priorites, exceptions et promotions de production. Il prevoit une offre Vercel Pro pour proteger recette et previews par mot de passe. Les agents fournissent des instructions et ne recoivent ni acces ni secret.
- Analytics : un module maison leger est envisage apres le MVP. Aucun traceur analytics ne sera integre au MVP sans nouvelle validation.
- Le MVP ne charge aucun analytics, publicite, suivi ni script tiers non justifie. Les principes WCAG 2.2 AA applicables sont l'objectif confirme.
- Mentions legales connues : NOCODE TESTING, SAS, SIREN 943 002 451, SIRET 943 002 451 00012, 8 ter rue de la penissiere, 85610 Cugand. L'adresse e-mail de confidentialite et les informations legales complementaires restent a confirmer avant publication.
- Les demandes de contact sont conservees au maximum trois ans apres le dernier contact actif, ou moins longtemps si la finalite est atteinte ou si la personne l'exige. Le commanditaire execute les suppressions. La politique de confidentialite doit etre relue par une personne competente avant publication.
- Aucun code applicatif, dependance, verrou de dependances, pipeline CI/CD ou configuration de deploiement n'est present a ce stade.

## Travaux en cours
- Les livrables exploratoires UX, test, securite, architecture et CI/CD sont rendus le 2026-09-20 ; ils attendent les arbitrages du commanditaire.
- Les dossiers `Processus/` et `qualite-logicielle/` ont ete crees le 2026-09-20. Toute integration GitHub Projects reste soumise a un lot technique explicite et a des droits dedies.

## Prochaines etapes
- Cadrer l'accueil/header et le formulaire `/contact/` a partir de la maquette et des US mises a jour.
- Implementer d'abord le transport local configurable, puis qualifier SMTP OVH en recette avant toute activation production.

## Historique utile
- L'ancienne base Docusaurus a ete retiree ; le depot repart d'une base propre.