# Pilotage projet — nocode-testing.com

Dernière mise à jour : 2026-09-20.

## Chantiers en cours

| Chantier | Agent | Modèle | Statut | Dépendances | Sortie attendue |
|---|---|---|---|---|---|
| Maquettes accueil + header expressives | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, choix attendu | Direction laboratoire et logo | `Orbite des cas` recommandée, `Champ de preuves` alternatif |
| Stratégie de test | Mikaya test | Claude Sonnet 4.5, repli GPT-5 | Complétée, validation attendue | Gouvernance GitHub et dossier qualité | Anomalies bloquantes/majeures interdisent production |
| Stratégie de test sécurité | Mina Cybersécurité | Claude Sonnet 4.5, repli GPT-5 | Complétée | SMTP OVH et rétention | Turnstile validé sous réserves, SMTP à qualifier en recette |
| Stack, architecture et CI/CD | Soso ArchiOps | Claude Sonnet 4.5, repli GPT-5 | Réévaluée, validation attendue | Plan Vercel et approbateurs | Eleventy et promotion humaine recommandés |
| Gouvernance produit / qualité | Scarce PO | Claude Sonnet 4.5, repli GPT-5 | Completee, validation d'usage attendue | Projects GitHub et arborescence | Dossier `qualite-logicielle/` cree, sans REQ, US, CT, campagne, execution ni anomalie fictifs |
| Processus projet | Soso ArchiOps | Claude Sonnet 4.5, repli GPT-5 | Complété | Gouvernance validée | Dossier `Processus/` et procédures opératoires créés |
| CAPTCHA | Mina Cybersécurité | Claude Sonnet 4.5, repli GPT-5 | Décision actée | Turnstile et flux formulaire | Turnstile validé sous réserves |
| Image puis maquette Atelier calibre | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, validation attendue | Brief UI validé | Direction et maquette « Labo puzzle » |
| Raffinement maquette hybride Atelier calibre | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, validation attendue | Retours UI détaillés | `assets/mockups/accueil-hybride-atelier-calibre.svg` : palette, logo visible et boutons personnalisés |
| Raffinement panneaux et boutons flat | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Terminé, validation attendue | Retours UI 7.14 | `assets/mockups/accueil-hybride-atelier-calibre-raffine.svg` et catalogue de formulations |
| Corrections panneaux et maquette sombre | Armindia UI | GPT-5, repli Claude Sonnet 4.5 | Validé | Retours UI 7.15 | Référence UI MVP : `accueil-puzzle-ateliers-themes.svg` |
| Politique de confidentialité | Mina Cybersécurité | Claude Sonnet 4.5, repli GPT-5 | Projet rédigé, relecture attendue | Rétention et flux connus | `Processus/11-projet-politique-confidentialite.md` |

## Tableau de bord

| Indicateur | Valeur | Statut |
|---|---:|---|
| User stories définies | 0 | Non démarré |
| Couverture TU | Non mesurable | Aucune stack ni suite de tests |
| Couverture TI/E2E | Non mesurable | Aucune stack ni suite de tests |
| Anomalies ouvertes | 0 connue | Aucun code applicatif |
| Risques sécurité / CVE ouverts | 0 CVE ; 2 réserves | SMTP/Vercel et secrets |
| Risques capacité / exploitation ouverts | 1 | SMTP/limitation à qualifier en recette |
| Tâches en attente de validation | 2 validations ciblées | Stack MVP et relecture juridique de la politique |

## Questions ouvertes

1. Validation de la stack MVP Eleventy + Node.js 22, avant développement.
2. Relecture humaine de la politique de confidentialité avant publication.
3. Validation du lot de cadrage produit accueil/header, avant création des exigences et tickets.